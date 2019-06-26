---
title: KSPROPERTY\_RTAUDIO\_REGISTER\_NOTIFICATION\_EVENT
description: KSPROPERTY\_RTAUDIO\_注册\_通知\_事件属性注册 DMA 驱动事件通知的用户模式事件。
ms.assetid: 8fd5883a-ff86-4d27-af44-a82511c9e8eb
keywords:
- KSPROPERTY_RTAUDIO_REGISTER_NOTIFICATION_EVENT 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_REGISTER_NOTIFICATION_EVENT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c414c418a8ff81e8ef3e15d61b064b5ae6df49d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358739"
---
# <a name="kspropertyrtaudioregisternotificationevent"></a>KSPROPERTY\_RTAUDIO\_REGISTER\_NOTIFICATION\_EVENT


KSPROPERTY\_RTAUDIO\_注册\_通知\_事件属性注册 DMA 驱动事件通知的用户模式事件。 必须在成功调用注册的事件[ **KSPROPERTY\_RTAUDIO\_缓冲区\_WITH\_通知**](ksproperty-rtaudio-buffer-with-notification.md)。

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
<td align="left"><p>是</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_notification_event_property" data-raw-source="[&lt;strong&gt;KSRTAUDIO_NOTIFICATION_EVENT_PROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_notification_event_property)"><strong>KSRTAUDIO_NOTIFICATION_EVENT_PROPERTY</strong></a></p></td>
<td align="left"><p><strong>NULL</strong></p></td>
</tr>
</tbody>
</table>

 

属性描述符 （实例数据） 包含 KSRTAUDIO\_通知\_事件\_包含的属性结构[ **KSPROPERTY** ](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))结构以及用户模式事件句柄。

此属性在属性值 （操作数据） **NULL**因为没有返回任何操作数据。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_ RTAUDIO\_注册\_通知\_事件属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的故障状态代码。 下表显示了一些可能的故障状态代码。

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
<td align="left"><p>STATUS_NOT_SUPPORTED</p></td>
<td align="left"><p>不支持事件通知。</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td align="left"><p>无法分配缓冲区的内存。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_DEVICE_NOT_READY</p></td>
<td align="left"><p>设备未就绪。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性用于注册 DMA 驱动事件通知的用户模式事件。

当 pin 放入*运行*状态 (KSSTATE\_运行) 的已注册的事件都已终止一次或两次每个循环的音频缓冲区的周期，具体取决于通知计数请求时 KSPROPERTY\_RTAUDIO\_缓冲区\_WITH\_通知调用。 有关 KSSTATERUN 详细信息，请参阅[状态转换](https://docs.microsoft.com/windows-hardware/drivers/stream/state-transitions)主题。

停止 pin，并在其关闭时的时间之前, 每个已注册的事件是通过调用未注册后[ **KSPROPERTY\_RTAUDIO\_注销\_通知\_事件**](ksproperty-rtaudio-unregister-notification-event.md).

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


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSPROPERTY\_RTAUDIO\_缓冲区\_WITH\_通知**](ksproperty-rtaudio-buffer-with-notification.md)

[**KSPROPERTY\_RTAUDIO\_注销\_通知\_事件**](ksproperty-rtaudio-unregister-notification-event.md)

[状态转换](https://docs.microsoft.com/windows-hardware/drivers/stream/state-transitions)

 

 






