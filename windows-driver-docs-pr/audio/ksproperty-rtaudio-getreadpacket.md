---
title: KSPROPERTY\_RTAUDIO\_GETREADPACKET
description: KSPROPERTY\_RTAUDIO\_GETREADPACKET 返回有关捕获音频的数据包的信息。
ms.assetid: BA52CDCE-0178-4C90-A82C-15800DD3709E
keywords:
- KSPROPERTY_RTAUDIO_GETREADPACKET 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_GETREADPACKET
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 12/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 99aebaa6f982d69670aa11172194fb2400e9c3eb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358752"
---
# <a name="kspropertyrtaudiogetreadpacket"></a>KSPROPERTY\_RTAUDIO\_GETREADPACKET


KSPROPERTY\_RTAUDIO\_GETREADPACKET 返回有关捕获音频的数据包的信息。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

 
|Get|设置|目标|属性描述符类型|属性值类型|
|--- |--- |--- |--- |--- |
|是|否|Pin|[KSPROPERTY](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))|[KSRTAUDIO_GETREADPACKET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_getreadpacket_info)|


属性描述符 （实例数据） 是[ **KSPROPERTY** ](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))结构。 发送请求之前, 在客户端加载具有值，用于指示数据包编号、 数据包长度和其他信息的结构。

属性值是类型的变量[ **KSRTAUDIO\_GETREADPACKET\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_getreadpacket_info)。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_RTAUDIO\_GETREADPACKET 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的故障状态代码。

状态\_设备\_不\_准备就绪的驱动程序返回此错误，如果没有任何新数据可用。

<a name="remarks"></a>备注
-------

读取捕获 WaveRT 缓冲区中的音频数据之前，操作系统将调用此例程，以获取有关可用数据的信息。

数据包编号标识流中的数据包。 这将重置为零流 KSSTATE 时\_停止。 与每个捕获缓冲区前移数。 从数据包编号操作系统可以派生 WaveRT 缓冲区中的数据包位置，并可派生的数据包相对启动流的流位置。

数据包大小是 WaveRT 缓冲区大小除以传递给 NotificationCount [ **KSPROPERTY\_RTAUDIO\_缓冲区\_WITH\_通知**](ksproperty-rtaudio-buffer-with-notification.md). 操作系统可能会在任何时候调用此例程。 在正常操作中，OS 将调用此例程驱动程序设置缓冲区通知事件后或在上一次调用为 MoreData 返回 true。 当操作系统调用此例程时，该驱动程序可能会假定操作系统已完成读取以前的所有数据包。 如果硬件已捕获足够的数据，该驱动程序可能会立即迸发到 WaveRT 缓冲区的下一步完成数据包并再次设置缓冲区事件。 对于捕获溢出 （当操作系统不会足够快速地读取数据） 的音频驱动程序可能会删除或覆盖一些音频数据。 音频驱动程序将删除或首先将覆盖最旧的数据，音频驱动程序可能会继续前进的内部数据包计数器，即使操作系统可能不具有读取数据。

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
<td align="left"><p>在 Windows 10 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY\_RTAUDIO\_SETWRITEPACKET**](ksproperty-rtaudio-setwritepacket.md)

[UsePositionLock](usepositionlock.md)

 

 






