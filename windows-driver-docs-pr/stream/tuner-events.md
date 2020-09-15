---
title: 调谐器事件
description: 调谐器事件
ms.assetid: eb5e0698-2641-4d47-9fa3-d1969a03c795
keywords:
- 调谐器事件 WDK 视频捕获
- 事件 WDK 视频捕获
- EVENTSETID_TUNER
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ccf7ca429b12add6d89294b0e5820f758860102
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104404"
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

 

