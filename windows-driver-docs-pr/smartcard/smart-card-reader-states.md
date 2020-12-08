---
title: 智能卡读卡器状态
description: 智能卡读卡器状态
keywords:
- 智能卡驱动程序 WDK，读卡器状态
- 读者状态 WDK 智能卡
- 状态 WDK 智能卡
- 供应商提供的驱动程序 WDK 智能卡，读卡器状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45dc8549772de5898ac1b3ade7a4881eafd5c62f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804875"
---
# <a name="smart-card-reader-states"></a>智能卡读卡器状态


## <span id="_ntovr_smart_card_reader_states"></span><span id="_NTOVR_SMART_CARD_READER_STATES"></span>


下表定义了智能卡读卡器状态。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状态</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SCARD_UNKNOWN</p></td>
<td align="left"><p>指示读取器驱动程序没有有关读取器的当前状态的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SCARD_ABSENT</p></td>
<td align="left"><p>指示读取器中没有卡片。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SCARD_PRESENT</p></td>
<td align="left"><p>指示读卡器中存在卡，但尚未将其移动到位置以供使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SCARD_SWALLOWED</p></td>
<td align="left"><p>指示卡在读卡器中并且要使用的位置。 卡未通电。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SCARD_POWERED</p></td>
<td align="left"><p>指示卡已通电，但读卡器驱动程序没有与卡状态有关的其他信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SCARD_NEGOTIABLE</p></td>
<td align="left"><p>指示该卡已重置并正在等待磅协商。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SCARD_SPECIFIC</p></td>
<td align="left"><p>指示已重置卡，并且已建立特定的通信协议。</p></td>
</tr>
</tbody>
</table>

 

 

 





