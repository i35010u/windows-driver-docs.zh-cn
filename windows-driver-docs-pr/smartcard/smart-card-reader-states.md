---
title: 智能卡读卡器状态
description: 智能卡读卡器状态
ms.assetid: 7596ba27-206a-4590-aec0-c9009e7a12b6
keywords:
- 智能卡驱动程序 WDK，读取器状态
- 读取器状态 WDK 智能卡
- 状态 WDK 智能卡
- 供应商提供的驱动程序 WDK 智能卡读取器状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75d8c9a777c878d8cdf682cfbe964bb47e2d58c1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382537"
---
# <a name="smart-card-reader-states"></a>智能卡读卡器状态


## <span id="_ntovr_smart_card_reader_states"></span><span id="_NTOVR_SMART_CARD_READER_STATES"></span>


下表定义的智能卡读取器状态。

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
<td align="left"><p>指示读卡器驱动程序，有没有关于读取器的当前状态的信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SCARD_ABSENT</p></td>
<td align="left"><p>指示读取器中没有卡。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SCARD_PRESENT</p></td>
<td align="left"><p>指示卡读取器中出现，但它不已移到使用的位置。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SCARD_SWALLOWED</p></td>
<td align="left"><p>指示一个卡读取器在和中使用的位置。 卡不提供支持。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SCARD_POWERED</p></td>
<td align="left"><p>指示此卡提供支持，但读卡器驱动程序具有的卡片的状态的任何其他信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SCARD_NEGOTIABLE</p></td>
<td align="left"><p>指示此卡已被重置，并在等待 PTS 协商。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SCARD_SPECIFIC</p></td>
<td align="left"><p>指示卡已被重置，并且建立了特定通信协议。</p></td>
</tr>
</tbody>
</table>

 

 

 





