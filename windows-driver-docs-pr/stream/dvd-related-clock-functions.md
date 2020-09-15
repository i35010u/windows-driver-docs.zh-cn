---
title: 与 DVD 相关的时钟函数
description: 与 DVD 相关的时钟函数
ms.assetid: 495f25dc-cd79-4f7f-acbc-b8b271269fb3
keywords:
- DVD 解码器微型驱动程序 WDK，主时钟
- 解码器微型驱动程序 WDK DVD，主时钟
- 主时钟 WDK DVD 解码器
- 时钟 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1cc41ada5034dc63f53740fce1c2292d91782b6
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103328"
---
# <a name="dvd-related-clock-functions"></a>与 DVD 相关的时钟函数





所有时钟句柄都应与相应的单个流一起存储。 它们不应存储在全局或静态变量中。 有关详细信息，请参阅 [KS 时钟](ks-clocks.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/srb-open-master-clock" data-raw-source="[&lt;strong&gt;SRB_OPEN_MASTER_CLOCK&lt;/strong&gt;](./srb-open-master-clock.md)"><strong>SRB_OPEN_MASTER_CLOCK</strong></a></p></td>
<td><p>向 DVD 解码器微型驱动程序指定的流将作为主时钟打开，并提供一个主时钟句柄，以用于对 DVD 解码器微型驱动程序主时钟例程的所有调用以访问该时钟。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/stream/srb-close-master-clock" data-raw-source="[&lt;strong&gt;SRB_CLOSE_MASTER_CLOCK&lt;/strong&gt;](./srb-close-master-clock.md)"><strong>SRB_CLOSE_MASTER_CLOCK</strong></a></p></td>
<td><p>指示指定的主时钟句柄不再处于活动状态。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/stream/srb-indicate-master-clock" data-raw-source="[&lt;strong&gt;SRB_INDICATE_MASTER_CLOCK&lt;/strong&gt;](./srb-indicate-master-clock.md)"><strong>SRB_INDICATE_MASTER_CLOCK</strong></a></p></td>
<td><p>指示在调用时间戳并向所有流提供时要使用的句柄。</p></td>
</tr>
</tbody>
</table>

 

