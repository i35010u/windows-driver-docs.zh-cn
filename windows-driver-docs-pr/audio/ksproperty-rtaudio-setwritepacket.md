---
title: KSPROPERTY\_RTAUDIO\_SETWRITEPACKET
description: KSPROPERTY\_RTAUDIO\_SETWRITEPACKET 告知驱动程序 OS 已向 WaveRT 缓冲区写入有效的数据。
ms.assetid: 2827D6BC-B669-4AAC-967C-99B068DCC29B
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
ms.openlocfilehash: 4da46e8ff07c9d733834cf6ee23b3454e7e7b958
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523751"
---
# <a name="kspropertyrtaudiosetwritepacket"></a>KSPROPERTY\_RTAUDIO\_SETWRITEPACKET


KSPROPERTY\_RTAUDIO\_SETWRITEPACKET 告知驱动程序 OS 已向 WaveRT 缓冲区写入有效的数据。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

|Get|设置|目标|属性描述符类型|属性值类型|
|--- |--- |--- |--- |--- |
|否|是|Pin|[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)|[KSRTAUDIO_SETWRITEPACKET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_setwritepacket_info)|


属性描述符 （实例数据） 是[ **KSPROPERTY** ](https://msdn.microsoft.com/library/windows/hardware/ff564262)结构。 发送请求之前, 在客户端加载值包含数据包编号、 数据包长度和其他信息的结构。

属性值是类型的结构[ **KSRTAUDIO\_SETWRITEPACKET\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksrtaudio_setwritepacket_info)。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_RTAUDIO\_SETWRITEPACKET 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的故障状态代码。

<a name="remarks"></a>备注
-------

如果支持此 KSPROPERTY，则该驱动程序可能会选择使用所提供的信息来优化硬件传输。 例如，驱动程序可能会优化 DMA 传输或程序硬件 OS 不会调用此例程再次以通知另一个数据包的驱动程序的情况下停止末尾指定数据包的传输。 这可以降低声音效果的下溢，例如引入有声间隙而不是重复一个循环缓冲区。 该驱动程序但是是仍有义务增加其内部的数据包计数器和信号通知事件名义实时的速度。

除操作系统时指定*KSSTREAM\_标头\_OPTIONSF\_ENDOFSTREAM*标志，数据包大小是 WaveRT 缓冲区大小除以传递给 NotificationCount [**KSPROPERTY\_RTAUDIO\_缓冲区\_WITH\_通知**](ksproperty-rtaudio-buffer-with-notification.md)。

根据硬件功能，如果*KSSTREAM\_标头\_OPTIONSF\_ENDOFSTREAM*指定标志，该驱动程序可能会静默填充遵循 EOS WaveRT 缓冲区的一部分用例在硬件中的数据包将传输超出 EOS 位置的数据。

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
<td align="left"><p>在 Windows 10 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSPROPERTY\_RTAUDIO\_GETREADPACKET**](ksproperty-rtaudio-getreadpacket.md)

[UsePositionLock](usepositionlock.md)

 

 






