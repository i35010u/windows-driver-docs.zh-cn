---
title: 驱动程序的浮点注释
description: 批注可以帮助检测的浮点使用的代码分析工具的浮点数在内核模式代码点和可以报告错误，如果未正确保护的浮点状态。 仅对内核模式代码检查浮点规则。
ms.assetid: 86FF1A21-674F-4BDA-AC03-C1E5F06A4439
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45f5d626d7c43d231514d92b98d96671e6a03754
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329707"
---
# <a name="floating-point-annotations-for-drivers"></a>驱动程序的浮点注释


批注可以帮助检测的浮点使用的代码分析工具的浮点数在内核模式代码点和可以报告错误，如果未正确保护的浮点状态。 仅对内核模式代码检查浮点规则。

了解某些处理器系列，尤其是 x86 处理器，使用浮点运算从内核模式代码中的必须完成的范围内仅函数的保存和还原浮点状态。 违反此规则可以是特别困难地发现，因为它们仅偶尔会在运行时导致问题 （但这些问题可以是非常严重）。 使用正确的批注，代码分析工具能够有效地检测内核模式代码中的浮动点和报告错误，如果未正确保护浮点状态。 仅对内核模式代码检查浮点规则。

将以下注释添加到函数参数，以指示它们与浮点状态执行的操作。

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
<td align="left"><p>带批注的函数时该函数将返回已成功保存浮点硬件状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_Kernel_float_restored_"></span><span id="_kernel_float_restored_"></span><span id="_KERNEL_FLOAT_RESTORED_"></span><em>Kernel_float_restored</em></p></td>
<td align="left"><p>带批注的函数时该函数将返回已成功还原浮点硬件状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="_Kernel_float_used_"></span><span id="_kernel_float_used_"></span><span id="_KERNEL_FLOAT_USED_"></span><em>Kernel_float_used</em></p></td>
<td align="left"><p>如果调用函数安全地调用该函数，则可以使用<em>Kernel_float_used</em>要禁止显示错误的报告中的批注。 但是，如果调用的函数还没有批注与<em>Kernel_float_used</em>或函数调用不会使用批注的函数之间发生<em>Kernel_float_saved 和 _Kernel_float_restored</em>，分别，代码分析工具将报告错误。</p></td>
</tr>
</tbody>
</table>



这些批注已应用于 KeSaveFloatingPoint 状态和 KeRestoreFloatingPointState 系统函数，除了获取和释放资源，以防止泄漏的批注。 在这种方式中还批注类似 EngXxx 函数。 但是，包装这些函数的函数还应使用这些批注。

如果某些调用函数安全地调用该函数作为一个整体，可以使用批注函数\_内核\_float\_使用\_批注。 这将禁止显示警告，同时也导致代码分析工具来确认调用方安全地使用该函数。 更高级别的\_内核\_float\_使用\_可以添加所需的方式。 \_内核\_float\_使用\_批注将自动提供的代码分析工具时函数结果或函数的参数之一是浮点点类型，但它不会不会降低到显式提供批注。

例如，\_内核\_float\_保存\_批注指示，KeSaveFloatingPointState 系统函数的 FloatingState 参数中存储浮点状态。

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

在以下示例中，\_内核\_float\_使用\_批注禁止使用浮点状态有关的警告。 批注也会导致代码分析工具来确认对 MyDoesFloatingPoint 的任何调用发生在安全的浮点上下文中。

```
_Kernel_float_used_
void
    MyDoesFloatingPoint(arguments);
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[Windows 驱动程序的 SAL 2.0 注释](sal-2-annotations-for-windows-drivers.md)










