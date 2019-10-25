---
title: KSPROPERTY\_RTAUDIO\_缓冲器\_与\_通知
description: 使用\_通知属性的 KSPROPERTY\_RTAUDIO\_BUFFER\_指定用于音频数据的驱动程序分配的循环缓冲区，并标识事件通知要求。下表汇总了此属性的功能。
ms.assetid: a66727ae-03d6-41b5-b5c9-3b04352b3b83
keywords:
- KSPROPERTY_RTAUDIO_BUFFER_WITH_NOTIFICATION 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_BUFFER_WITH_NOTIFICATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4340fb69a238f1bc31618a999efca8fc6a8e131
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830696"
---
# <a name="ksproperty_rtaudio_buffer_with_notification"></a>KSPROPERTY\_RTAUDIO\_缓冲器\_与\_通知


使用\_通知属性的 KSPROPERTY\_RTAUDIO\_BUFFER\_指定用于音频数据的驱动程序分配的循环缓冲区，并标识事件通知要求。

下表汇总了此属性的功能。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

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
<th align="left">“获取”</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>“是”</p></td>
<td align="left"><p>无</p></td>
<td align="left"><p>大头针</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_buffer_property_with_notification" data-raw-source="[&lt;strong&gt;KSRTAUDIO_BUFFER_PROPERTY_WITH_NOTIFICATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_buffer_property_with_notification)"><strong>KSRTAUDIO_BUFFER_PROPERTY_WITH_NOTIFICATION</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_buffer" data-raw-source="[&lt;strong&gt;KSRTAUDIO_BUFFER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_buffer)"><strong>KSRTAUDIO_BUFFER</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性说明符（实例数据）包含一个 KSRTAUDIO\_缓冲区\_属性\_和\_通知结构，其中包含与其他成员一起使用的[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))结构。 客户端将其请求的缓冲区大小写入结构中。 除非需要特定的基址，否则客户端必须将基址指定为**NULL** 。

当你需要 DMA 驱动的事件通知时，将使用此属性。 基于**NotificationCount**成员，已注册的事件在循环缓冲区中每循环发出一次（在结束时）或两次（在 mid 和 end）。 使用[**KSPROPERTY\_RTAUDIO\_注册\_通知\_事件**](ksproperty-rtaudio-register-notification-event.md)的事件在成功调用 KSPROPERTY\_RTAUDIO\_使用\_通知的缓冲区\_后，注册通知事件。

属性值（操作数据）是[**KSRTAUDIO\_BUFFER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_buffer)类型的结构。 驱动程序将用其已分配的循环缓冲区的实际缓冲区大小、基址和内存屏障标志填充此结构。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

带有\_通知属性请求的 KSPROPERTY\_RTAUDIO\_缓冲器\_返回状态\_SUCCESS 以指示已成功完成。 否则，请求将返回相应的失败状态代码。 下表显示了某些可能的失败状态代码。

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
<td align="left"><p>无法为具有指定的缓冲区属性组合的循环缓冲区分配。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td align="left"><p>无法为缓冲区分配内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_DEVICE_NOT_READY</p></td>
<td align="left"><p>设备未就绪。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

基址是循环缓冲区开头的虚拟内存地址。 客户端可以直接访问此地址处的缓冲区。 缓冲区在虚拟内存中是连续的。 驱动程序确定缓冲区是否在物理内存中是连续的。

客户端将属性描述符中的基址设置为**NULL**。 驱动程序将属性值中的基址设置为分配的音频缓冲区的虚拟地址。

通常情况下，音频硬件要求音频缓冲区在示例边界开始和结束，或满足其他类型的硬件相关的对齐约束。 如果有足够的内存可用，则缓冲区的实际大小将为请求的大小舍入（向上或向下）到最接近的样本或其他硬件约束边界。 否则，实际大小可以小于请求的大小。

如果 KSPROPERTY\_RTAUDIO\_BUFFER\_与\_通知属性请求成功，则属性值是 KSRTAUDIO\_BUFFER 类型的结构，它包含驱动程序分配的缓冲区的地址和大小。

关闭 pin 会自动释放通过此属性分配的缓冲区。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSRTAUDIO\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_buffer)

[**KSRTAUDIO\_缓冲区\_属性\_与\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_buffer_property_with_notification)

[**KSPROPERTY\_RTAUDIO\_注册\_通知\_事件**](ksproperty-rtaudio-register-notification-event.md)

 

 






