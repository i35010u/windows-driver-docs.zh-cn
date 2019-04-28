---
title: KSEVENT\_LOOPEDSTREAMING\_位置
description: KSEVENT\_LOOPEDSTREAMING\_位置事件指示音频流已到达循环缓冲区中的指定的位置。使用情况摘要 TableTargetEvent 描述符 TypeEvent 值 TypePinKSEVENTLOOPEDSTREAMING\_位置\_事件\_数据的事件值类型 （操作数据） 是 LOOPEDSTREAMING\_位置\_事件\_数据结构，其中包含以下信息的位置事件发生时，系统将向客户端发送的通知类型。触发事件缓冲区位置。
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
ms.openlocfilehash: 1c2db83ad4be87df7cdff1b7bb496971e659173b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333359"
---
# <a name="kseventloopedstreamingposition"></a>KSEVENT\_LOOPEDSTREAMING\_位置


KSEVENT\_LOOPEDSTREAMING\_位置事件指示音频流已到达循环缓冲区中的指定的位置。

**使用率摘要表**

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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561744" data-raw-source="[&lt;strong&gt;KSEVENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561744)"><strong>KSEVENT</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537505" data-raw-source="[&lt;strong&gt;LOOPEDSTREAMING_POSITION_EVENT_DATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537505)"><strong>LOOPEDSTREAMING_POSITION_EVENT_DATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

事件值类型 （操作数据） 是 LOOPEDSTREAMING\_位置\_事件\_数据结构，其中包含以下信息：

-   位置事件发生时，系统将向客户端发送的通知的类型。

-   触发事件缓冲区位置。

此事件旨在由系统仅供内部使用。

<a name="remarks"></a>备注
-------

在 Windows Server 2003、 Windows XP、 Windows 2000、 Windows Me 和 Windows 98，WavePci 和 WaveCyclic 端口驱动程序包含自己的内置处理程序为 KSEVENT\_LOOPEDSTREAMING\_位置事件。 WavePci 和 WaveCyclic 微型端口驱动程序不应实现这些事件处理程序。

在 Windows Vista 中，没有任何批*Xxx*端口驱动程序实现事件处理程序或其他支持 KSEVENT\_LOOPEDSTREAMING\_位置事件。

一个循环的缓冲区就是类型的音频流的数据缓冲区[ **KSINTERFACE\_标准\_LOOPED\_流式处理**](https://msdn.microsoft.com/library/windows/hardware/ff563381)。 当播放或录制光标达到循环缓冲区的末尾时，光标回绕到缓冲区的开头。

有关循环的缓冲区、 缓冲区位置，并播放和记录游标的详细信息，请参阅[音频 Position 属性](https://msdn.microsoft.com/library/windows/hardware/ff536211)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSEVENT**](https://msdn.microsoft.com/library/windows/hardware/ff561744)

[**KSINTERFACE\_标准\_LOOPED\_流式处理**](https://msdn.microsoft.com/library/windows/hardware/ff563381)

[**LOOPEDSTREAMING\_POSITION\_EVENT\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff537505)

 

 






