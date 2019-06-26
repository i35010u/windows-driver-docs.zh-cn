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
ms.openlocfilehash: b7d3844389ce57a4d65976902f6ae0f2a9a6c252
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377717"
---
# <a name="tuner-events"></a>调谐器事件


[EVENTSETID\_调谐器](https://docs.microsoft.com/windows-hardware/drivers/stream/eventsetid-tuner)事件集中包含调谐器事件。 下表描述了属于 EVENTSETID 事件\_调谐器事件集。 第二个表描述了为运行 Windows Vista 及更高版本 AVStream 微型驱动程序实现一个调谐器事件。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>EVENTSETID_TUNER KS 事件</th>
<th>事件描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-tuner-changed" data-raw-source="[&lt;strong&gt;KSEVENT_TUNER_CHANGED&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-tuner-changed)"><strong>KSEVENT_TUNER_CHANGED</strong></a></p></td>
<td><p>DirectShow 调谐器已更改，例如，由于调到新的电视频道的通知。</p></td>
</tr>
</tbody>
</table>

 

下表描述了 EVENTSETID\_调谐器事件适用于 Windows Vista 新增的。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>EVENTSETID_TUNER KS 事件</th>
<th>事件描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-tuner-initiate-scan" data-raw-source="[&lt;strong&gt;KSEVENT_TUNER_INITIATE_SCAN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-tuner-initiate-scan)"><strong>KSEVENT_TUNER_INITIATE_SCAN</strong></a></p></td>
<td><p>启动信号扫描，扫描完成时通知 DirectShow。</p></td>
</tr>
</tbody>
</table>

 

 

 




