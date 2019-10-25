---
title: KSPROPERTY\_RTAUDIO\_注册\_通知\_事件
description: KSPROPERTY\_RTAUDIO\_REGISTER\_通知\_事件属性为 DMA 驱动的事件通知注册用户模式事件。
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
ms.openlocfilehash: d4368b035acb6fa01c5d63dda2a404e91574cbd5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830596"
---
# <a name="ksproperty_rtaudio_register_notification_event"></a>KSPROPERTY\_RTAUDIO\_注册\_通知\_事件


KSPROPERTY\_RTAUDIO\_REGISTER\_通知\_事件属性为 DMA 驱动的事件通知注册用户模式事件。 成功调用[**带有\_通知的 KSPROPERTY\_RTAUDIO\_缓冲器\_** ](ksproperty-rtaudio-buffer-with-notification.md)后，必须注册事件。

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
<td align="left"><p>“是”</p></td>
<td align="left"><p>大头针</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_notification_event_property" data-raw-source="[&lt;strong&gt;KSRTAUDIO_NOTIFICATION_EVENT_PROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_notification_event_property)"><strong>KSRTAUDIO_NOTIFICATION_EVENT_PROPERTY</strong></a></p></td>
<td align="left"><p><strong>无效</strong></p></td>
</tr>
</tbody>
</table>

 

属性说明符（实例数据）包含一个 KSRTAUDIO\_通知\_事件\_属性结构，其中包含一个[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))结构以及一个用户模式事件句柄。

此属性的属性值（操作数据）为**NULL** ，因为没有返回操作数据。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_ RTAUDIO\_REGISTER\_通知\_事件属性请求返回状态\_SUCCESS 以指示已成功完成。 否则，请求将返回相应的失败状态代码。 下表显示了某些可能的失败状态代码。

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

此属性用于为 DMA 驱动的事件通知注册用户模式事件。

当将 pin 置于*运行*状态（KSSTATE\_run）时，每次循环音频缓冲区的每个周期发出一次或两次通知已注册的事件，具体取决于 KSPROPERTY\_RTAUDIO\_缓冲区时请求的通知计数 @no__调用了 t_4_\_通知。 有关 KSSTATERUN 的详细信息，请参阅[状态转换](https://docs.microsoft.com/windows-hardware/drivers/stream/state-transitions)主题。

停止 pin 后，在关闭 pin 之前，会通过对 KSPROPERTY\_RTAUDIO 的调用取消注册每个注册事件， [ **\_取消注册\_通知\_事件**](ksproperty-rtaudio-unregister-notification-event.md)。

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

[**KSPROPERTY\_RTAUDIO\_缓冲器\_与\_通知**](ksproperty-rtaudio-buffer-with-notification.md)

[**KSPROPERTY\_RTAUDIO\_注销\_通知\_事件**](ksproperty-rtaudio-unregister-notification-event.md)

[状态转换](https://docs.microsoft.com/windows-hardware/drivers/stream/state-transitions)

 

 






