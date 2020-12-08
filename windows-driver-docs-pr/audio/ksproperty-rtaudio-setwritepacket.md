---
title: KSPROPERTY \_ RTAUDIO \_ SETWRITEPACKET
description: KSPROPERTY \_ RTAUDIO \_ SETWRITEPACKET 通知驱动程序操作系统已将有效数据写入 WaveRT 缓冲区。
keywords:
- KSPROPERTY_RTAUDIO_SETWRITEPACKET 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_SETWRITEPACKET
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 12/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: d18fc428bc23a9c70d01e70ec13e98478e91ef77
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801181"
---
# <a name="ksproperty_rtaudio_setwritepacket"></a>KSPROPERTY \_ RTAUDIO \_ SETWRITEPACKET


KSPROPERTY \_ RTAUDIO \_ SETWRITEPACKET 通知驱动程序操作系统已将有效数据写入 WaveRT 缓冲区。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

|获取|设置|目标|属性描述符类型|属性值类型|
|--- |--- |--- |--- |--- |
|否|是|Pin|[**KSPROPERTY**](/previous-versions/ff564262(v=vs.85))|[KSRTAUDIO_SETWRITEPACKET_INFO](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_setwritepacket_info)|


属性描述符 (实例数据) 是 [**KSPROPERTY**](/previous-versions/ff564262(v=vs.85)) 结构。 在发送请求之前，客户端会加载包含数据包编号、数据包长度和其他信息的值的结构。

属性值为 [**KSRTAUDIO \_ SETWRITEPACKET \_ INFO**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_setwritepacket_info)类型的结构。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ RTAUDIO \_ SETWRITEPACKET 属性请求返回状态 \_ SUCCESS 以指示该请求已成功完成。 否则，请求将返回相应的失败状态代码。

<a name="remarks"></a>备注
-------

如果支持此 KSPROPERTY，则驱动程序可能会选择使用提供的信息来优化硬件传输。 例如，驱动程序可能会优化 DMA 传输，或在指定数据包结束时停止传输，以防操作系统再次调用此例程来通知其他数据包的驱动程序。 这可以减少下溢的声音效果，例如引入可听见的间隙，而不是重复循环缓冲区。 然而，驱动程序仍有义务以额定的实时速率增加其内部数据包计数器和信号通知事件。

除非 OS 指定 *KSSTREAM \_ 标头 \_ OPTIONSF \_ ENDOFSTREAM* 标志，否则，数据包大小为 WaveRT 的缓冲区大小，该大小除以传递到 [**NotificationCount \_ KSPROPERTY 缓冲区 \_ 的 \_ \_ 通知**](ksproperty-rtaudio-buffer-with-notification.md)。

根据硬件功能，如果指定了 *KSSTREAM \_ 标头 \_ OPTIONSF \_ ENDOFSTREAM* 标志，驱动程序可能会在硬件传输超出 eos 位置的数据的情况下，不的部分 WaveRT 缓冲区。

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


[**KSPROPERTY \_ RTAUDIO \_ GETREADPACKET**](ksproperty-rtaudio-getreadpacket.md)

[UsePositionLock](usepositionlock.md)

 

