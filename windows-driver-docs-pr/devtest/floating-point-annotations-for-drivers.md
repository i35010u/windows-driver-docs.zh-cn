---
title: 驱动程序的浮点注释
description: 浮点批注可帮助代码分析工具在内核模式代码中检测浮点的使用情况，并且如果未正确保护浮点状态，则可以报告错误。 仅对内核模式代码检查浮点规则。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 328ce35519ab5082b2c6ff808de710bbc5481046
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839757"
---
# <a name="floating-point-annotations-for-drivers"></a>驱动程序的浮点注释


浮点批注可帮助代码分析工具在内核模式代码中检测浮点的使用情况，并且如果未正确保护浮点状态，则可以报告错误。 仅对内核模式代码检查浮点规则。

对于某些处理器系列，尤其是 x86 处理器，只能在保存和还原浮点状态的函数范围内完成使用内核模式代码中的浮点运算。 此规则的冲突可能特别难找到，因为它们只会在运行时偶尔导致问题 (但这些问题可能非常严重) 。 通过正确使用批注，代码分析工具有效地检测内核模式代码中的浮点使用情况，并在未正确保护浮点状态时报告错误。 仅对内核模式代码检查浮点规则。

将以下批注添加到函数参数，以指示它们对浮点状态执行的操作。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">浮点批注</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="_Kernel_float_saved_"></span><span id="_kernel_float_saved_"></span><span id="_KERNEL_FLOAT_SAVED_"></span><em>Kernel_float_saved</em></p></td>
<td align="left"><p>当函数成功返回时，带批注的函数将保存浮点硬件状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_Kernel_float_restored_"></span><span id="_kernel_float_restored_"></span><span id="_KERNEL_FLOAT_RESTORED_"></span><em>Kernel_float_restored</em></p></td>
<td align="left"><p>当函数成功返回时，带批注的函数将还原浮点硬件状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="_Kernel_float_used_"></span><span id="_kernel_float_used_"></span><span id="_KERNEL_FLOAT_USED_"></span><em>Kernel_float_used</em></p></td>
<td align="left"><p>如果调用函数安全调用该函数，则可以使用 <em>Kernel_float_used</em> 注释来取消报告错误。 但是，如果调用函数尚未同时用 <em>Kernel_float_used</em> 进行批注，或在 <em>Kernel_float_saved 和 _Kernel_float_restored</em>批注的函数之间不发生函数调用，则代码分析工具将报告错误。</p></td>
</tr>
</tbody>
</table>



除了获取和释放资源以防止泄漏外，这些批注还已应用于 KeSaveFloatingPoint 状态和 KeRestoreFloatingPointState 系统函数。 类似的 EngXxx 函数也以这种方式进行批注。 但包装这些函数的函数还应使用这些注释。

如果通过某个调用函数安全地调用了整个函数，则可以使用 \_ 内核 \_ 浮点 \_ 使用批注对该函数进行批注 \_ 。 这将禁止显示警告，并导致代码分析工具确认调用方安全地使用函数。 \_ \_ \_ 可以根据需要添加其他级别的内核 float \_ 。 \_ \_ \_ \_ 当函数结果或函数的某个参数为浮点类型时，代码分析工具会自动提供内核浮点使用批注，但不会损害显式提供批注。

例如， \_ 内核 \_ 浮点保存的 \_ \_ 批注指示浮点状态存储在 KeSaveFloatingPointState 系统函数的 FloatingState 参数中。

```ManagedCPlusPlus
_Must_inspect_result_  
_IRQL_requires_max_(DISPATCH_LEVEL)  
__drv_valueIs(<0;==0)  
_When_(return==0, _Kernel_float_saved_)  
_At_(*FloatingState, _Kernel_requires_resource_not_held_(FloatState) _When_(return==0, _Kernel_acquires_resource_(FloatState)))  
__forceinline  
NTSTATUS  
KeSaveFloatingPointState (  
    _Out_ PVOID FloatingState  
    )  
```

在下面的示例中，" \_ 内核 \_ 浮点 \_ 使用批注" 取消了 \_ 有关使用浮点状态的警告。 批注还会导致代码分析工具确认在安全浮点上下文中发生对 MyDoesFloatingPoint 的任何调用。

```
_Kernel_float_used_
void
    MyDoesFloatingPoint(arguments);
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[Windows 驱动程序的 SAL 2.0 注释](sal-2-annotations-for-windows-drivers.md)










