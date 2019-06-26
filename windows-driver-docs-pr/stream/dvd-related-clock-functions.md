---
title: 与 DVD 相关的时钟函数
description: 与 DVD 相关的时钟函数
ms.assetid: 495f25dc-cd79-4f7f-acbc-b8b271269fb3
keywords:
- DVD 解码器微型驱动程序 WDK，主时钟
- 解码器微型驱动程序 WDK DVD，主时钟
- 主时钟 WDK DVD 解码器
- 时钟的 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73dfe7ab923b05866060743b1abfd4f2df49d0e4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384146"
---
# <a name="dvd-related-clock-functions"></a>与 DVD 相关的时钟函数





应与相应的单个流存储所有时钟句柄。 单元测试不应存储在全局或静态变量中。 有关详细信息，请参阅[KS 时钟](ks-clocks.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/srb-open-master-clock" data-raw-source="[&lt;strong&gt;SRB_OPEN_MASTER_CLOCK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-open-master-clock)"><strong>SRB_OPEN_MASTER_CLOCK</strong></a></p></td>
<td><p>表示到 DVD 解码器微型驱动程序指定的流正在打开作为主时钟，并且提供用于访问该时钟的所有调入 DVD 解码器微型驱动程序主时钟例程上的主时钟句柄。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/srb-close-master-clock" data-raw-source="[&lt;strong&gt;SRB_CLOSE_MASTER_CLOCK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-close-master-clock)"><strong>SRB_CLOSE_MASTER_CLOCK</strong></a></p></td>
<td><p>指示指定的主时钟句柄不再处于活动状态。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/stream/srb-indicate-master-clock" data-raw-source="[&lt;strong&gt;SRB_INDICATE_MASTER_CLOCK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-indicate-master-clock)"><strong>SRB_INDICATE_MASTER_CLOCK</strong></a></p></td>
<td><p>指示要调用的时间戳时使用的句柄提供给所有流。</p></td>
</tr>
</tbody>
</table>

 

 

 




