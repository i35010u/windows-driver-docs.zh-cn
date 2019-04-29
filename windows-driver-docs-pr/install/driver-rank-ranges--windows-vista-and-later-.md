---
title: 驱动程序分级范围
description: 驱动程序分级范围
ms.assetid: ea822171-c1f3-49b4-ae63-3300728666f0
keywords:
- 驱动程序级别范围 WDK 设备安装
- 排名范围 WDK 设备安装
- 范围排名 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ae40fb83399ff1a8b68f2347d54b6d392dc1d77
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356009"
---
# <a name="driver-rank-ranges"></a>驱动程序分级范围


驱动程序级别的格式设置为 0x*SSGGTHHH*，其中值 0x*SS*000000 是[签名分数](signature-score--windows-vista-and-later-.md)，值 0x00*GG*0000 是[功能分数](feature-score--windows-vista-and-later-.md)，和 0x0000 值*THHH*是[标识符分数](identifier-score--windows-vista-and-later-.md)。

下表列出了所有有效的驱动程序排名范围，其中 0 x*SS*000000 表示有效的签名分数，0x00*GG*0000 表示有效的功能得分和标识符的范围为评分显示每种类型的标识符匹配。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">驱动程序级别</th>
<th align="left">标识符分数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0xSS<em>GG</em>0000-0xSS<em>GG</em>0FFF</p></td>
<td align="left"><p>0x0000-0x0FFF</p></td>
<td align="left"><p>设备硬件 ID 匹配的硬件 ID 在 INF<em>模型</em>部分项。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xSS<em>GG</em>1000-0xSS<em>GG</em>1FFF</p></td>
<td align="left"><p>0x1000-0x1FFF</p></td>
<td align="left"><p>设备硬件 ID 匹配的兼容 ID 以 INF<em>模型</em>部分项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xSS<em>GG</em>2000-0xSS<em>GG</em>2FFF</p></td>
<td align="left"><p>0x2000-0x2FFF</p></td>
<td align="left"><p>设备兼容 ID 匹配的硬件 ID 在 INF<em>模型</em>部分项。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xSS<em>GG</em>3000-0xSS<em>GG</em>3FFF</p></td>
<td align="left"><p>0x3000-0x3FFF</p></td>
<td align="left"><p>设备兼容 ID 匹配的兼容 ID 以 INF<em>模型</em>部分项。</p></td>
</tr>
</tbody>
</table>

 

 

 





