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
ms.openlocfilehash: 32a738879c95cfb3d4654bae447025d87394e1be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519889"
---
# <a name="tuner-events"></a>调谐器事件


[EVENTSETID\_调谐器](https://msdn.microsoft.com/library/windows/hardware/ff559566)事件集中包含调谐器事件。 下表描述了属于 EVENTSETID 事件\_调谐器事件集。 第二个表描述了为运行 Windows Vista 及更高版本 AVStream 微型驱动程序实现一个调谐器事件。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561894" data-raw-source="[&lt;strong&gt;KSEVENT_TUNER_CHANGED&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561894)"><strong>KSEVENT_TUNER_CHANGED</strong></a></p></td>
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561898" data-raw-source="[&lt;strong&gt;KSEVENT_TUNER_INITIATE_SCAN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561898)"><strong>KSEVENT_TUNER_INITIATE_SCAN</strong></a></p></td>
<td><p>启动信号扫描，扫描完成时通知 DirectShow。</p></td>
</tr>
</tbody>
</table>

 

 

 




