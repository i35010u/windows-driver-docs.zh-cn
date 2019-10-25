---
title: KSEVENT\_LOOPEDSTREAMING\_位置
description: KSEVENT\_LOOPEDSTREAMING\_位置事件指示音频流已到达循环缓冲区中的指定位置。使用情况摘要 TableTargetEvent 描述符 TypeEvent 值 TypePinKSEVENTLOOPEDSTREAMING\_位置\_事件\_数据事件值类型（操作数据）是 LOOPEDSTREAMING\_位置\_事件\_数据结构，其中包含以下信息：当位置事件发生时系统将发送到客户端的通知的类型。触发事件的缓冲区位置。
ms.assetid: 6609ddac-e506-4fab-b580-0def30be2e9c
keywords:
- KSEVENT_LOOPEDSTREAMING_POSITION 音频设备
topic_type:
- apiref
api_name:
- KSEVENT_LOOPEDSTREAMING_POSITION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 941c651f54369090bf05892cda10465056f51fe7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833140"
---
# <a name="ksevent_loopedstreaming_position"></a>KSEVENT\_LOOPEDSTREAMING\_位置


KSEVENT\_LOOPEDSTREAMING\_位置事件指示音频流已到达循环缓冲区中的指定位置。

**使用情况摘要表**

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">目标</th>
<th align="left">事件描述符类型</th>
<th align="left">事件值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>大头针</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff561744(v=vs.85)" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))"><strong>KSEVENT</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-loopedstreaming_position_event_data" data-raw-source="[&lt;strong&gt;LOOPEDSTREAMING_POSITION_EVENT_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-loopedstreaming_position_event_data)"><strong>LOOPEDSTREAMING_POSITION_EVENT_DATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

事件值类型（操作数据）是 LOOPEDSTREAMING\_位置\_事件\_数据结构，其中包含以下信息：

-   出现位置事件时系统将发送到客户端的通知的类型。

-   触发事件的缓冲区位置。

此事件仅供系统内部使用。

<a name="remarks"></a>备注
-------

在 Windows Server 2003、Windows XP、windows 2000、Windows Me 和 Windows 98 中，WavePci 和 WaveCyclic 端口驱动程序包含它们自己的用于 KSEVENT\_LOOPEDSTREAMING\_位置事件的内置处理程序。 WavePci 和 WaveCyclic 微型端口驱动程序不应为这些事件实现处理程序。

在 Windows Vista 中，无 Wave*Xxx*端口驱动程序实现事件处理程序或其他对 KSEVENT\_LOOPEDSTREAMING\_位置事件的支持。

循环缓冲区是类型为[**KSINTERFACE\_标准\_循环\_流式处理**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksinterface-standard-looped-streaming)的音频流的数据缓冲区。 当播放或记录光标到达循环缓冲区的末尾时，游标将环绕到缓冲区的开头。

有关循环缓冲区、缓冲区位置以及播放和记录游标的详细信息，请参阅[音频位置属性](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-position-property)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSEVENT**](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))

[**KSINTERFACE\_标准\_循环\_流式处理**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksinterface-standard-looped-streaming)

[**LOOPEDSTREAMING\_位置\_事件\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-loopedstreaming_position_event_data)

 

 






