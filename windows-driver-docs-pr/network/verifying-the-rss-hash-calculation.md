---
title: 验证 RSS 哈希计算
description: 验证 RSS 哈希计算
keywords:
- 接收方缩放 WDK 网络，哈希
- RSS WDK 网络，哈希
- 哈希 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1705b9ca24d79de581382c932a65cd8fcca52a46
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822105"
---
# <a name="verifying-the-rss-hash-calculation"></a>验证 RSS 哈希计算





你应验证是否实现了 RSS 哈希计算。 若要验证 **NdisHashFunctionToeplitz** 哈希函数的计算，请使用以下密钥数据：

```syntax
0x6d, 0x5a, 0x56, 0xda, 0x25, 0x5b, 0x0e, 0xc2,
0x41, 0x67, 0x25, 0x3d, 0x43, 0xa3, 0x8f, 0xb0,
0xd0, 0xca, 0x2b, 0xcb, 0xae, 0x7b, 0x30, 0xb4,
0x77, 0xcb, 0x2d, 0xa3, 0x80, 0x30, 0xf2, 0x0c,
0x6a, 0x42, 0xb7, 0x3b, 0xbe, 0xac, 0x01, 0xfa
```

下表提供了 IPv4 版本的 **NdisHashFunctionToeplitz** 哈希函数的验证数据。 "目标" 和 "源" 列包含输入数据，IPv4 列包含结果哈希值。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">目标地址:P o</th>
<th align="left">源地址:P o</th>
<th align="left">仅 IPv4</th>
<th align="left">带有 TCP 的 IPv4</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>161.142.100.80：1766</p></td>
<td align="left"><p>66.9.149.187：2794</p></td>
<td align="left"><p>0x323e8fc2</p></td>
<td align="left"><p>0x51ccc178</p></td>
</tr>
<tr class="even">
<td align="left"><p>65.69.140.83：4739</p></td>
<td align="left"><p>199.92.111.2：14230</p></td>
<td align="left"><p>0xd718262a</p></td>
<td align="left"><p>0xc626b0ea</p></td>
</tr>
<tr class="odd">
<td align="left"><p>12.22.207.184：38024</p></td>
<td align="left"><p>24.19.198.95：12898</p></td>
<td align="left"><p>0xd2d0a5de</p></td>
<td align="left"><p>0x5c2b394a</p></td>
</tr>
<tr class="even">
<td align="left"><p>209.142.163.6：2217</p></td>
<td align="left"><p>38.27.205.30：48228</p></td>
<td align="left"><p>0x82989176</p></td>
<td align="left"><p>0xafc7327f</p></td>
</tr>
<tr class="odd">
<td align="left"><p>202.188.127.2：1303</p></td>
<td align="left"><p>153.39.163.191：44251</p></td>
<td align="left"><p>0x5d1809c5</p></td>
<td align="left"><p>0x10e828a2</p></td>
</tr>
</tbody>
</table>

 

下表包含 RSS 哈希算法的 IPv6 版本的验证数据。 "目标" 和 "源" 列包含输入数据，IPv6 列包含生成的哈希值。 请注意，提供的 IPv6 地址仅用于验证算法;它们可能并不是实际地址。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">目标地址 (端口) </th>
<th align="left"> (端口) 的源地址</th>
<th align="left">仅 IPv6</th>
<th align="left">带有 TCP 的 IPv6</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>3ffe：2501：200：3：： 1 (1766) </p></td>
<td align="left"><p>3ffe：2501：200：1fff：： 7 (2794) </p></td>
<td align="left"><p>0x2cc18cd5</p></td>
<td align="left"><p>0x40207d3d</p></td>
</tr>
<tr class="even">
<td align="left"><p>ff02：： 1 (4739) </p></td>
<td align="left"><p>3ffe：501：8：：260：97ff： fe40： efab (14230) </p></td>
<td align="left"><p>0x0f0c461c</p></td>
<td align="left"><p>0xdde51bbf</p></td>
</tr>
<tr class="odd">
<td align="left"><p>fe80：：200： f8ff： fe21： 67cf (38024) </p></td>
<td align="left"><p>3ffe：1900：4545：3：200： f8ff： fe21： 67cf (44251) </p></td>
<td align="left"><p>0x4b61e985</p></td>
<td align="left"><p>0x02d1feef</p></td>
</tr>
</tbody>
</table>

 

 

 





