---
title: DVD 解码器相关 KS 事件
description: DVD 解码器相关 KS 事件
ms.assetid: 19fd2c88-72f4-4742-8c96-74be250dd59d
keywords:
- DVD 解码器微型驱动程序 WDK，KS 事件
- 解码器微型驱动程序 WDK DVD，KS 事件
- KS 事件 WDK DVD 解码器
- 事件的 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 276342417ba8ab8697c83eec3a4304c0c5035bb7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543363"
---
# <a name="dvd-decoder-related-ks-events"></a>DVD 解码器相关 KS 事件





下表描述了流式处理事件集和其相应的事件与 DVD 解码器硬件相关的内核：

[KSEVENTSETID\_VPNotify](https://msdn.microsoft.com/library/windows/hardware/ff561780)组流式处理与调谐器事件相关的事件的所有内核事件都设置。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561933" data-raw-source="[&lt;strong&gt;KSEVENT_VPNOTIFY_FORMATCHANGE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561933)"><strong>KSEVENT_VPNOTIFY_FORMATCHANGE</strong></a></p></td>
<td><p>通知 DirectShow 中的视频端口配置，如从 640 x 480 到 720 x 480 解析中的更改的更改。</p></td>
</tr>
</tbody>
</table>

 

 

 




