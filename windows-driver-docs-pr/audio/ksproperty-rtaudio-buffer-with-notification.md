---
title: '\_ \_ \_ 带有通知的 KSPROPERTY RTAUDIO 缓冲区 \_'
description: '\_ \_ 带有 NOTIFICATION 属性的 KSPROPERTY RTAUDIO 缓冲区 \_ \_ 指定用于音频数据的驱动程序分配的循环缓冲区，并标识事件通知要求。下表汇总了此属性的功能。'
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
ms.openlocfilehash: 62878a453e6cfbd3a36daf1bcb24d7253bdaa06c
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101966"
---
# <a name="ksproperty_rtaudio_buffer_with_notification"></a>\_ \_ \_ 带有通知的 KSPROPERTY RTAUDIO 缓冲区 \_


\_ \_ 带有 NOTIFICATION 属性的 KSPROPERTY RTAUDIO 缓冲区 \_ \_ 指定用于音频数据的驱动程序分配的循环缓冲区，并标识事件通知要求。

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
<th align="left">获取</th>
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
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_buffer_property_with_notification" data-raw-source="[&lt;strong&gt;KSRTAUDIO_BUFFER_PROPERTY_WITH_NOTIFICATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_buffer_property_with_notification)"><strong>KSRTAUDIO_BUFFER_PROPERTY_WITH_NOTIFICATION</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_buffer" data-raw-source="[&lt;strong&gt;KSRTAUDIO_BUFFER&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_buffer)"><strong>KSRTAUDIO_BUFFER</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性描述符 (实例数据) 包含 \_ \_ \_ \_ 包含通知结构的 KSRTAUDIO 缓冲区属性以及其他成员。 [**KSPROPERTY**](/previous-versions/ff564262(v=vs.85)) 客户端将其请求的缓冲区大小写入结构中。 除非需要特定的基址，否则客户端必须将基址指定为 **NULL** 。

当你需要 DMA 驱动的事件通知时，将使用此属性。 基于 **NotificationCount** 成员，已注册的事件将在结束后 (收到) 或两次 (，并在循环缓冲区中按循环) 结束。 成功调用带有通知的 KSPROPERTY RTAUDIO 缓冲区后，将使用 [**KSPROPERTY \_ RTAUDIO \_ REGISTER \_ 通知 \_ 事件**](ksproperty-rtaudio-register-notification-event.md) 注册事件 \_ \_ \_ \_ 。

 (操作数据) 的属性值是 [**KSRTAUDIO \_ 缓冲区**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_buffer)类型的结构。 驱动程序将用其已分配的循环缓冲区的实际缓冲区大小、基址和内存屏障标志填充此结构。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

\_ \_ \_ 带有通知属性请求的 KSPROPERTY RTAUDIO 缓冲区 \_ 返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的失败状态代码。 下表显示了某些可能的失败状态代码。

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
<td align="left"><p>设备未准备就绪。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

基址是循环缓冲区开头的虚拟内存地址。 客户端可以直接访问此地址处的缓冲区。 缓冲区在虚拟内存中是连续的。 驱动程序确定缓冲区是否在物理内存中是连续的。

客户端将属性描述符中的基址设置为 **NULL**。 驱动程序将属性值中的基址设置为分配的音频缓冲区的虚拟地址。

通常情况下，音频硬件要求音频缓冲区在示例边界开始和结束，或满足其他类型的硬件相关的对齐约束。 如果有足够的内存可用，则缓冲区的实际大小为 (向上或向下舍入到最接近的样本或其他硬件约束的边界时，所请求的大小) 。 否则，实际大小可以小于请求的大小。

如果 \_ \_ \_ 带有 NOTIFICATION 属性请求的 KSPROPERTY RTAUDIO 缓冲区 \_ 成功，则属性值（是 KSRTAUDIO 缓冲区类型的结构 \_ ）包含驱动程序分配的缓冲区的地址和大小。

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


[**KSPROPERTY**](/previous-versions/ff564262(v=vs.85))

[**KSRTAUDIO \_ 缓冲区**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_buffer)

[**\_ \_ \_ 带有通知的 KSRTAUDIO BUFFER 属性 \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_buffer_property_with_notification)

[**KSPROPERTY \_ RTAUDIO \_ 注册 \_ 通知 \_ 事件**](ksproperty-rtaudio-register-notification-event.md)

