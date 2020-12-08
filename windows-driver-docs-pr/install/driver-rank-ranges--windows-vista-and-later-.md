---
title: 驱动程序分级范围
description: 驱动程序分级范围
keywords:
- 驱动程序排名范围 WDK 设备安装
- 排名范围 WDK 设备安装
- 范围排名 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c24ba11f75dd304399e4a4dbe2cb13389d7b856e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782713"
---
# <a name="driver-rank-ranges"></a>驱动程序分级范围


驱动程序级别的格式设置为 0x *SSGGTHHH*，其中 0x *SS* 000000 的值是 [签名分数](signature-score--windows-vista-and-later-.md)，0x00 *GG* 0000 的值是 [功能分数](feature-score--windows-vista-and-later-.md)，0x0000 *THHH* 的值是 [标识符分数](identifier-score--windows-vista-and-later-.md)。

下表列出了所有有效的驱动程序排名范围，其中 0x *SS* 000000 表示有效的签名分数，0x00 *GG* 0000 表示有效的功能分数，并显示了每种类型的标识符匹配的标识符分数范围。

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
<td align="left"><p>0xSS<em>gg</em>0000-0xSS<em>GG</em>0FFF</p></td>
<td align="left"><p>0x0000-0x0FFF</p></td>
<td align="left"><p>设备硬件 ID 与 "INF <em>模型</em> " 部分条目中的硬件 id 匹配。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xSS<em>gg</em>1000-0xSS<em>GG</em>1FFF</p></td>
<td align="left"><p>0x1000-0x1FFF</p></td>
<td align="left"><p>设备硬件 ID 与 INF <em>模型</em> 部分条目中的兼容 ID 匹配。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xSS<em>gg</em>2000-0xSS<em>GG</em>2FFF</p></td>
<td align="left"><p>0x2000-0x2FFF</p></td>
<td align="left"><p>与 INF <em>模型</em> 部分条目中的硬件 id 匹配的设备兼容 ID。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xSS<em>gg</em>3000-0xSS<em>GG</em>3FFF</p></td>
<td align="left"><p>0x3000-0x3FFF</p></td>
<td align="left"><p>设备兼容 ID 与 INF <em>模型</em> 部分条目中的兼容 id 匹配。</p></td>
</tr>
</tbody>
</table>

 

 

 





