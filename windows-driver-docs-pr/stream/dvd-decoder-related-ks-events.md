---
title: 与 DVD 解码器相关的 KS 事件
description: 与 DVD 解码器相关的 KS 事件
ms.assetid: 19fd2c88-72f4-4742-8c96-74be250dd59d
keywords:
- DVD 解码器微型驱动程序 WDK，KS 事件
- 解码器微型驱动程序 WDK DVD，KS 事件
- KS 事件 WDK DVD 解码器
- 事件的 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51595a2596dd53cb34821e23439a6f1e1bfa64f8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387164"
---
# <a name="dvd-decoder-related-ks-events"></a>与 DVD 解码器相关的 KS 事件





下表描述了流式处理事件集和其相应的事件与 DVD 解码器硬件相关的内核：

[KSEVENTSETID\_VPNotify](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-vpnotify)组流式处理与调谐器事件相关的事件的所有内核事件都设置。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>KSEVENTSETID_VPNotify KS 事件</th>
<th>事件描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-vpnotify-formatchange" data-raw-source="[&lt;strong&gt;KSEVENT_VPNOTIFY_FORMATCHANGE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-vpnotify-formatchange)"><strong>KSEVENT_VPNOTIFY_FORMATCHANGE</strong></a></p></td>
<td><p>通知 DirectShow 中的视频端口配置，如从 640 x 480 到 720 x 480 解析中的更改的更改。</p></td>
</tr>
</tbody>
</table>

 

 

 




