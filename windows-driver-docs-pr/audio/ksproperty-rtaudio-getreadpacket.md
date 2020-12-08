---
title: KSPROPERTY \_ RTAUDIO \_ GETREADPACKET
description: KSPROPERTY \_ RTAUDIO \_ GETREADPACKET 返回有关捕获的音频数据包的信息。
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
ms.openlocfilehash: 1adbcf467e62a11d59400f94e6aeb739980a7757
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801193"
---
# <a name="ksproperty_rtaudio_getreadpacket"></a>KSPROPERTY \_ RTAUDIO \_ GETREADPACKET


KSPROPERTY \_ RTAUDIO \_ GETREADPACKET 返回有关捕获的音频数据包的信息。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

 
|获取|设置|目标|属性描述符类型|属性值类型|
|--- |--- |--- |--- |--- |
|是|否|Pin|[KSPROPERTY](/previous-versions/ff564262(v=vs.85))|[KSRTAUDIO_GETREADPACKET_INFO](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_getreadpacket_info)|


属性描述符 (实例数据) 是 [**KSPROPERTY**](/previous-versions/ff564262(v=vs.85)) 结构。 在发送请求之前，客户端将加载包含指示数据包编号、数据包长度和其他信息的值的结构。

属性值是 [**KSRTAUDIO \_ GETREADPACKET \_ INFO**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_getreadpacket_info)类型的变量。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ RTAUDIO \_ GETREADPACKET 属性请求返回状态 \_ SUCCESS 以指示该请求已成功完成。 否则，请求将返回相应的失败状态代码。

状态 \_ 设备 \_ 未 \_ 就绪-如果没有新数据可用，驱动程序将返回此错误。

<a name="remarks"></a>备注
-------

在从 WaveRT 缓冲区读取捕获的音频数据之前，操作系统将调用此例程以获取有关可用数据的信息。

数据包编号标识流中的数据包。 当流处于 KSSTATE 停止时，这会重置为零 \_ 。 每个捕获的缓冲区的数目会提升。 从数据包编号中，OS 可以在 WaveRT 缓冲区内派生数据包位置，还可以派生出数据包相对于流起始位置的流位置。

数据包大小是 WaveRT 缓冲区大小除以传递到 [**KSPROPERTY RTAUDIO 缓冲区的 NotificationCount， \_ \_ \_ 并 \_ 通知**](ksproperty-rtaudio-buffer-with-notification.md)。 操作系统可以随时调用此例程。 在正常操作中，当驱动程序设置缓冲区通知事件之后，或在上一次调用为 MoreData 返回 true 后，操作系统将调用此例程。 当 OS 调用此例程时，驱动程序可能会假设 OS 已读取完以前的所有数据包。 如果硬件捕获了足够的数据，驱动程序可能会立即将下一个完整的数据包爆发到 WaveRT 缓冲区，并再次设置 buffer 事件。 在捕获溢出的情况下 (当操作系统没有足够快地读取数据时) 音频驱动程序可能会删除或覆盖某些音频数据。 音频驱动程序会先删除或覆盖最早的数据，音频驱动程序可能会继续提升其内部数据包计数器，即使 OS 可能没有读取数据。

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
<td align="left"><p>适用于 Windows 10 及更高版本的 Windows 操作系统。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY \_ RTAUDIO \_ SETWRITEPACKET**](ksproperty-rtaudio-setwritepacket.md)

[UsePositionLock](usepositionlock.md)

 

