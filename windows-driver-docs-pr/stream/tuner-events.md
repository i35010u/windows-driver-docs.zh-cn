---
title: 调谐器事件
description: 调谐器事件
keywords:
- 调谐器事件 WDK 视频捕获
- 事件 WDK 视频捕获
- EVENTSETID_TUNER
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e340b2ba0c89b1d0268008cadd0ae67be4c94baf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783721"
---
# <a name="tuner-events"></a>调谐器事件


[EVENTSETID \_ 调谐器](./eventsetid-tuner.md)事件集包含调谐器事件。 下表描述了属于 EVENTSETID \_ 调谐器事件集的事件。 第二个表描述了为在 Windows Vista 和更高版本上运行的 AVStream 微型驱动程序实现的调谐器事件。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>EVENTSETID_TUNER KS 事件</th>
<th>事件说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksevent-tuner-changed" data-raw-source="[&lt;strong&gt;KSEVENT_TUNER_CHANGED&lt;/strong&gt;](./ksevent-tuner-changed.md)"><strong>KSEVENT_TUNER_CHANGED</strong></a></p></td>
<td><p>向 DirectShow 发出信号，指示调谐器发生了变化，例如，由于对新的电视频道进行了调整。</p></td>
</tr>
</tbody>
</table>

 

下表描述了适用 \_ 于 Windows Vista 的 EVENTSETID 调谐器事件。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>EVENTSETID_TUNER KS 事件</th>
<th>事件说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/ksevent-tuner-initiate-scan" data-raw-source="[&lt;strong&gt;KSEVENT_TUNER_INITIATE_SCAN&lt;/strong&gt;](./ksevent-tuner-initiate-scan.md)"><strong>KSEVENT_TUNER_INITIATE_SCAN</strong></a></p></td>
<td><p>启动信号扫描并在扫描完成时通知 DirectShow。</p></td>
</tr>
</tbody>
</table>

 

