---
title: KSPROPERTY\_RTAUDIO\_缓冲区
description: KSPROPERTY\_RTAUDIO\_缓冲区属性指定驱动程序分配的音频数据的循环缓冲区。下表总结了此属性的功能。
ms.assetid: e2c78849-1a34-446c-9f44-012f36ddafa5
keywords:
- KSPROPERTY_RTAUDIO_BUFFER 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_BUFFER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4aff71afda39ff3646c3277d6f29f23d970e96b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332687"
---
# <a name="kspropertyrtaudiobuffer"></a>KSPROPERTY\_RTAUDIO\_缓冲区


KSPROPERTY\_RTAUDIO\_缓冲区属性指定驱动程序分配的音频数据的循环缓冲区。

下表总结了此属性的功能。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Get</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="ksrtaudio-buffer-property.md" data-raw-source="[&lt;strong&gt;KSRTAUDIO_BUFFER_PROPERTY&lt;/strong&gt;](ksrtaudio-buffer-property.md)"><strong>KSRTAUDIO_BUFFER_PROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537493" data-raw-source="[&lt;strong&gt;KSRTAUDIO_BUFFER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537493)"><strong>KSRTAUDIO_BUFFER</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性描述符 （实例数据） 包含 KSRTAUDIO\_缓冲区\_属性结构，其中包含[ **KSPROPERTY** ](https://msdn.microsoft.com/library/windows/hardware/ff564262)结构以及其他成员。 客户端将写入到结构其请求的缓冲区大小。 如果客户端不需要使用特定基址，它必须指定为基址**NULL**。

属性值 （操作数据） 是一种结构的类型 KSRTAUDIO\_缓冲区。 该驱动程序填充此结构与实际的缓冲区大小、 基址和它已经分配了循环缓冲区的内存屏障标志。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_RTAUDIO\_缓冲区属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的故障状态代码。 下表显示了一些可能的故障状态代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状态代码</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_UNSUCCESSFUL</p></td>
<td align="left"><p>无法分配缓冲区属性的指定组合循环缓冲区。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td align="left"><p>无法分配缓冲区的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_DEVICE_NOT_READY</p></td>
<td align="left"><p>设备未就绪</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

基址是在循环缓冲区开头的虚拟内存地址。 客户端可以直接访问此地址处的缓冲区。 缓冲区是连续虚拟内存中。 决定是否要在物理内存中连续缓冲区应由驱动程序。

客户端应为属性描述符中设置的基址**NULL**。 该驱动程序分配的音频缓冲区的虚拟地址的属性值中设置的基址。

通常情况下，音频硬件所需的音频缓冲区来开始和结束的示例边界或满足其他类型的依赖于硬件的对齐约束。 如果有足够的内存可用，缓冲区的实际大小是所请求的大小 （向上或向下） 舍入到最接近的示例或其他硬件约束的边界。 实际大小必须至少为所请求的大小;否则为音频会话 API （wasapi 就可以了） 音频引擎不会使用缓冲区，并且流创建将失败。

如果 KSPROPERTY\_RTAUDIO\_缓冲区属性请求已成功提交，属性值，该值是一个结构类型 KSRTAUDIO\_缓冲区中包含的地址和驱动程序分配的缓冲区的大小。

自动关闭 pin 释放已通过此属性分配的缓冲区。

如果你想事件通知，则必须调用[ **KSPROPERTY\_RTAUDIO\_缓冲区\_WITH\_通知**](ksproperty-rtaudio-buffer-with-notification.md)而不是 KSPROPERTY\_RTAUDIO\_缓冲区。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSRTAUDIO\_BUFFER**](https://msdn.microsoft.com/library/windows/hardware/ff537493)

[**KSRTAUDIO\_缓冲区\_属性**](ksrtaudio-buffer-property.md)

[**KSPROPERTY\_RTAUDIO\_缓冲区\_WITH\_通知**](ksproperty-rtaudio-buffer-with-notification.md)

 

 






