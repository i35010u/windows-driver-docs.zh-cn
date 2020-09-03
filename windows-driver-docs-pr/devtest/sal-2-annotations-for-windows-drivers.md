---
title: Windows 驱动程序的 SAL 2.0 注释
description: Microsoft 源代码批注语言 (SAL) 包含特定于 Windows 驱动程序分析和相关内核代码的注释。
ms.assetid: 2CD181B8-4E1D-457A-9FF9-DAB3AB932730
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7526d36a9725f3c470dc6f53d7f17012ac1f1a2d
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381869"
---
# <a name="sal-20-annotations-for-windows-drivers"></a>Windows 驱动程序的 SAL 2.0 注释


Microsoft 源代码批注语言 (SAL) 包含特定于 Windows 驱动程序分析和相关内核代码的注释。 批注语言提供了一种方法来描述函数、参数、返回值、结构和结构字段的属性。 批注类似于添加到代码中并被编译器忽略但由静态分析工具使用的注释。 使用批注有助于提高开发人员的工作效率，帮助提高静态分析的结果准确性，并使工具能够更好地确定是否存在特定的 bug。 驱动程序批注不适用于非驱动程序或非内核相关的代码。 驱动程序批注是在 Driverspecs 中定义的。

**注意**   Windows 8 引入了 SAL 2.0，后者替代了 SAL 1.0。 有关 SAL 2.0 的信息，请参阅 [使用 Sal 注释减少 C/c + + 代码缺陷](/cpp/code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects)。 SAL 2.0 替换 SAL 1.0。 对于 Windows 8，应将 SAL 2.0 与适用于 windows 8)  (的 Windows 驱动程序工具包结合使用。 如果需要有关 SAL 1.0 的驱动程序的信息，请参阅 WDK for Windows 7 随附的文档。

 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">驱动程序批注</th>
<th align="left">类别</th>
<th align="left">用途</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>IRQL_requires_max</em></strong> (<em>值</em>) </p>
<p><strong><em>IRQL_requires_min</em></strong> (<em>值</em>) </p>
<p><strong><em>IRQL_raises</em></strong> (<em>值</em>) </p>
<p><strong><em>IRQL_requires</em></strong> (<em>值</em>) </p>
<p><strong><em>IRQL_raises</em></strong> (<em>值</em>) </p>
<p><strong><em>IRQL_saves</em></strong></p>
<p><strong><em>IRQL_restores</em></strong></p>
<p><strong><em>IRQL_saves_global</em></strong> (<em>kind</em>) <em>param</em></p>
<p><strong><em>IRQL_restores_global</em></strong> (<em>kind</em>) <em>param</em></p>
<p><strong><em>IRQL_always_function_min</em></strong> (<em>值</em>) </p>
<p><strong><em>IRQL_always_function_max</em></strong> (<em>值</em>) </p>
<p><strong><em>IRQL_requires_same</em></strong></p></td>
<td align="left"><a href="irql-annotations-for-drivers.md" data-raw-source="[IRQL annotations](irql-annotations-for-drivers.md)">IRQL 批注</a></td>
<td align="left"><p>使用 IRQL 批注指定函数应在其上运行的 IRQL 级别的范围。 IRQL 批注有助于代码分析工具更准确地查找错误。</p></td>
</tr>
<tr class="even">
<td align="left"><strong><em>IRQL_is_cancel</em></strong></td>
<td align="left"><a href="irql-annotations-for-drivers.md" data-raw-source="[IRQL annotations](irql-annotations-for-drivers.md)">IRQL 批注</a></td>
<td align="left"><p>使用 <em>IRQL_is_cancel</em> 批注有助于确保 <strong>DRIVER_CANCEL</strong> 回调函数的正确行为。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>Kernel_float_saved</em></strong></p>
<p><strong><em>Kernel_float_restored</em></strong></p>
<p><strong><em>Kernel_float_used</em></strong></p></td>
<td align="left"><a href="floating-point-annotations-for-drivers.md" data-raw-source="[Floating point annotations for drivers](floating-point-annotations-for-drivers.md)">驱动程序的浮点批注</a></td>
<td align="left"><p>使用浮点批注可帮助代码分析工具在内核模式代码中检测浮点的使用情况，并在未正确保护浮点状态时报告错误。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><em>Kernel_clear_do_init</em></strong></p></td>
<td align="left"><a href="do-device-initializing-annotation-for-drivers.md" data-raw-source="[DO_DEVICE_INITIALIZING annotation](do-device-initializing-annotation-for-drivers.md)">DO_DEVICE_INITIALIZING 批注</a></td>
<td align="left"><p>使用 <em>Kernel_clear_do_init</em> 批注指定是否应使用批注的函数清除设备对象的 "标志" 字段中的 DO_DEVICE_INITIALIZING 位。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>Kernel_IoGetDmaAdapter</em></strong></p></td>
<td align="left"><a href="-kernel-iogetdmaadapter--annotation-for-drivers.md" data-raw-source="[_Kernel_IoGetDmaAdapter_ Annotation](-kernel-iogetdmaadapter--annotation-for-drivers.md)"><em>Kernel_IoGetDmaAdapter</em> 绘图</a></td>
<td align="left"><p>使用 <em>Kernel_IoGetDmaAdapter</em> 注释指示代码分析工具查找是否误用 DMA 指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><em>Interlocked_operand</em></strong></p></td>
<td align="left"><a href="driver-annotations-for-interlocked-operands.md" data-raw-source="[Annotations for interlocked operands](driver-annotations-for-interlocked-operands.md)">联锁操作数的批注</a></td>
<td align="left"><p>使用函数参数 <em>Interlocked_operand</em> 批注将它们标识为互锁操作数。 许多函数作为其参数之一，这是一个变量的地址，该变量应使用联锁处理器指令进行访问。 这些是缓存读取原子说明，如果未正确使用操作数，则会产生非常微妙的 bug。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>Dispatch_type</em></strong></p></td>
<td align="left"><a href="declaring-functions-using-function-role-types-for-wdm-drivers.md#annotating_driver_dispatch_routines" data-raw-source="[Annotations for Driver Dispatch Routines](declaring-functions-using-function-role-types-for-wdm-drivers.md#annotating_driver_dispatch_routines)">驱动程序调度例程的注释</a>。</td>
<td align="left"><p>使用声明 WDM 驱动程序调度例程时使用的 <em>Dispatch_type</em> 注释。 请参阅 <a href="declaring-functions-using-function-role-types-for-wdm-drivers.md" data-raw-source="[Declaring Functions Using Function Role Types for WDM Drivers](declaring-functions-using-function-role-types-for-wdm-drivers.md)">使用 WDM 驱动程序的函数角色类型声明函数</a> 和 <a href="declaring-functions-using-function-role-types-for-wdm-drivers.md#annotating_driver_dispatch_routines" data-raw-source="[Annotating Driver Dispatch Routines](declaring-functions-using-function-role-types-for-wdm-drivers.md#annotating_driver_dispatch_routines)">批注驱动程序调度例程</a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><em>Flt_CompletionContext_Outptr</em></strong></p></td>
<td align="left"><a href="-flt-completioncontext-outptr--annotation.md" data-raw-source="[_Flt_CompletionContext_Outptr_ Annotation](-flt-completioncontext-outptr--annotation.md)"><em>Flt_CompletionContext_Outptr</em> 绘图</a></td>
<td align="left"><p>在声明文件系统微筛选器预操作回调函数 (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback" data-raw-source="[&lt;strong&gt;PFLT_PRE_OPERATION_CALLBACK&lt;/strong&gt;](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_pre_operation_callback)"><strong>PFLT_PRE_OPERATION_CALLBACK</strong></a>) 时使用<strong><em>Flt_CompletionContext_Outptr</em></strong>注释。 将此批注放置在 <em>CompletionContext</em> 参数上。 此批注指示代码分析工具检查 <em>CompletionContext</em> 是否适用于 FLT_PREOP_CALLBACK_STATUS 返回值。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[使用 SAL 注释减少 C/C++ 代码缺陷](/cpp/code-quality/using-sal-annotations-to-reduce-c-cpp-code-defects)

 

