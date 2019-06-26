---
title: Windows 驱动程序的 SAL 2.0 注释
description: Microsoft 源代码批注语言 (SAL) 包含特定于 Windows 驱动程序的分析和相关的内核代码的批注。
ms.assetid: 2CD181B8-4E1D-457A-9FF9-DAB3AB932730
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 871680ed9eae5a0a759ac295520aa64712f1dc27
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353862"
---
# <a name="sal-20-annotations-for-windows-drivers"></a>Windows 驱动程序的 SAL 2.0 注释


Microsoft 源代码批注语言 (SAL) 包含特定于 Windows 驱动程序的分析和相关的内核代码的批注。 批注语言提供了一种方法描述函数、 参数、 返回值、 结构和结构字段的属性。 批注是如注释将添加到你的代码和编译器忽略而由静态分析工具。 使用批注可帮助提高开发人员的工作效率、 可帮助提高静态分析的结果的准确性并允许以更好地确定是否存在某一特定错误的工具。 驱动程序批注不适用于非驱动程序或非内核相关的代码中使用。 驱动程序批注 Driverspecs.h 中定义。

**请注意**  Windows 8 引入了 SAL 2.0 中，它将替换 SAL 1.0。 有关 SAL 2.0 的信息，请参阅[使用 SAL 注释减少 C /C++代码缺陷](https://go.microsoft.com/fwlink/p/?linkid=247283)。 SAL 2.0 替换 SAL 1.0。 SAL 2.0 应使用与 Windows Driver Kit (WDK) 8 适用于 Windows 8。 如果驱动程序需要有关 SAL 1.0 的信息，请参阅随 Windows 7 的 WDK 文档。

 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">驱动程序批注</th>
<th align="left">Category</th>
<th align="left">将</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>IRQL_requires_max</em></strong>(<em>value</em>)</p>
<p><strong><em>IRQL_requires_min</em></strong>(<em>value</em>)</p>
<p><strong><em>IRQL_raises</em></strong>(<em>value</em>)</p>
<p><strong><em>IRQL_requires</em></strong>(<em>value</em>)</p>
<p><strong><em>IRQL_raises</em></strong>(<em>value</em>)</p>
<p><strong><em>IRQL_saves</em></strong></p>
<p><strong><em>IRQL_restores</em></strong></p>
<p><strong><em>IRQL_saves_global</em></strong>(<em>kind</em>, <em>param</em>)</p>
<p><strong><em>IRQL_restores_global</em></strong>(<em>kind</em>, <em>param</em>)</p>
<p><strong><em>IRQL_always_function_min</em></strong>(<em>value</em>)</p>
<p><strong><em>IRQL_always_function_max</em></strong>(<em>value</em>)</p>
<p><strong><em>IRQL_requires_same</em></strong></p></td>
<td align="left"><a href="irql-annotations-for-drivers.md" data-raw-source="[IRQL annotations](irql-annotations-for-drivers.md)">IRQL 批注</a></td>
<td align="left"><p>IRQL 批注用于指定应在其中运行函数的范围的 IRQL 级别。 IRQL 批注帮助以更准确地查找错误的代码分析工具。</p></td>
</tr>
<tr class="even">
<td align="left"><strong><em>IRQL_is_cancel</em></strong></td>
<td align="left"><a href="irql-annotations-for-drivers.md" data-raw-source="[IRQL annotations](irql-annotations-for-drivers.md)">IRQL 批注</a></td>
<td align="left"><p>使用<em>IRQL_is_cancel</em>批注可帮助确保正确行为<strong>DRIVER_CANCEL</strong>回调函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>Kernel_float_saved</em></strong></p>
<p><strong><em>Kernel_float_restored</em></strong></p>
<p><strong><em>Kernel_float_used</em></strong></p></td>
<td align="left"><a href="floating-point-annotations-for-drivers.md" data-raw-source="[Floating point annotations for drivers](floating-point-annotations-for-drivers.md)">浮动点批注的驱动程序</a></td>
<td align="left"><p>使用浮点点批注以帮助检测使用浮点数在内核模式代码并报告错误的浮点状态未正确地受到保护的代码分析工具。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><em>Kernel_clear_do_init</em></strong></p></td>
<td align="left"><a href="do-device-initializing-annotation-for-drivers.md" data-raw-source="[DO_DEVICE_INITIALIZING annotation](do-device-initializing-annotation-for-drivers.md)">DO_DEVICE_INITIALIZING 批注</a></td>
<td align="left"><p>使用<em>Kernel_clear_do_init</em>批注指定带批注的函数是否应清除 DO_DEVICE_INITIALIZING 位的设备对象的标志字段中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>Kernel_IoGetDmaAdapter</em></strong></p></td>
<td align="left"><a href="-kernel-iogetdmaadapter--annotation-for-drivers.md" data-raw-source="[_Kernel_IoGetDmaAdapter_ Annotation](-kernel-iogetdmaadapter--annotation-for-drivers.md)"><em>Kernel_IoGetDmaAdapter</em> Annotation</a></td>
<td align="left"><p>使用<em>Kernel_IoGetDmaAdapter</em>要直接查找不恰当使用 DMA 指针的代码分析工具中的批注。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><em>Interlocked_operand</em></strong></p></td>
<td align="left"><a href="driver-annotations-for-interlocked-operands.md" data-raw-source="[Annotations for interlocked operands](driver-annotations-for-interlocked-operands.md)">互锁操作数的批注</a></td>
<td align="left"><p>使用<em>Interlocked_operand</em>函数参数以标识为互锁操作数的批注。 多个函数将作为其参数之一应使用互锁的处理器指令进行访问的变量的地址。 这些是缓存直读原子说明，并且如果操作数使用不正确，导致非常难以发现的 bug。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>Dispatch_type</em></strong></p></td>
<td align="left"><a href="declaring-functions-using-function-role-types-for-wdm-drivers.md#annotating_driver_dispatch_routines" data-raw-source="[Annotations for Driver Dispatch Routines](declaring-functions-using-function-role-types-for-wdm-drivers.md#annotating_driver_dispatch_routines)">批注驱动程序的调度例程</a>。</td>
<td align="left"><p>使用<em>Dispatch_type</em>时声明 WDM 驱动程序调度例程使用的批注。 请参阅<a href="declaring-functions-using-function-role-types-for-wdm-drivers.md" data-raw-source="[Declaring Functions Using Function Role Types for WDM Drivers](declaring-functions-using-function-role-types-for-wdm-drivers.md)">函数用于 WDM 驱动程序函数的角色类型声明</a>和<a href="declaring-functions-using-function-role-types-for-wdm-drivers.md#annotating_driver_dispatch_routines" data-raw-source="[Annotating Driver Dispatch Routines](declaring-functions-using-function-role-types-for-wdm-drivers.md#annotating_driver_dispatch_routines)">批注驱动程序调度例程</a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><em>Flt_CompletionContext_Outptr</em></strong></p></td>
<td align="left"><a href="-flt-completioncontext-outptr--annotation.md" data-raw-source="[_Flt_CompletionContext_Outptr_ Annotation](-flt-completioncontext-outptr--annotation.md)"><em>Flt_CompletionContext_Outptr</em> Annotation</a></td>
<td align="left"><p>使用<strong><em>Flt_CompletionContext_Outptr</em></strong>批注时声明文件系统微筛选器预操作回调函数 (<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback" data-raw-source="[&lt;strong&gt;PFLT_PRE_OPERATION_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback)"><strong>PFLT_PRE_OPERATION_CALLBACK</strong></a>). 此批注置于<em>CompletionContext</em>参数。 此批注指示代码分析工具来检查是否<em>CompletionContext</em> FLT_PREOP_CALLBACK_STATUS 返回值是否正确。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[使用 SAL 注释减少 C/C++ 代码缺陷](https://go.microsoft.com/fwlink/p/?linkid=247283)

 

 






