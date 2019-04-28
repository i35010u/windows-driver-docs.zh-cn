---
title: 正在更新合并的段的 IP 标头
description: 本部分介绍如何更新合并的段的 IP 标头
ms.assetid: 18F2944A-D5A7-41BB-885F-EC183A00F7CE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62e99f33d7e13c78941b68d898866827f653a6a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340921"
---
# <a name="updating-the-ip-headers-for-coalesced-segments"></a>更新合并段的 IP 标头


正在最后完成单个合并单元 (SCU)，当接收段合并 (RSC)-支持微型端口驱动程序更新中的 IP 标头字段的以下表中所述。

-   [正在更新合并的段的 IPv4 标头字段](#updating-ipv4-header-fields-for-coalesced-segments)
-   [正在更新合并的段的 IPv6 标头字段](#updating-ipv6-header-fields-for-coalesced-segments)

## <a name="updating-ipv4-header-fields-for-coalesced-segments"></a>正在更新合并的段的 IPv4 标头字段


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>版本</strong></p></td>
<td align="left"><p>此字段的值必须是相同的所有合并的段。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>标头长度</strong></p></td>
<td align="left"><p>基本 IPv4 标头不包含任何 IP 选项的长度。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>差分的服务</strong></p></td>
<td align="left"><p>此字段的值必须是相同的所有合并的段。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ECN bits</strong></p></td>
<td align="left"><p>请参阅中的异常 8<a href="exception-conditions-that-terminate-coalescing.md" data-raw-source="[Exception Conditions that Terminate Coalescing](exception-conditions-that-terminate-coalescing.md)">终止合并的异常条件</a>。 如果它们都具有相同的 ECN 位的值应合并数据报。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>总长度</strong></p></td>
<td align="left"><p>每次新段 TCP 有效负载长度为非零值合并到现有 SCU 时，必须重新计算此字段的值。 请参阅<a href="exception-conditions-that-terminate-coalescing.md" data-raw-source="[Exception Conditions that Terminate Coalescing](exception-conditions-that-terminate-coalescing.md)">异常条件终止合并</a>的特殊情况所带来的此字段中的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Identification</strong></p></td>
<td align="left"><p>必须设置为第一个合并段 IP ID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>标志</strong></p></td>
<td align="left"><ul>
<li><p>可能会合并数据报，只要它们具有相同的值的 DF (Don't Fragment) 位： 所有设置或全部清除。</p></li>
<li><p>MF （更多段） 设置位的段必须不合并状态。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><strong>片段偏移量</strong></p></td>
<td align="left"><p>不适用。 不合并碎片的 IP 数据报。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>生存时间</strong></p></td>
<td align="left"><p>必须设置为最小时间生存的合并的段 (TTL) 值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Protocol</strong></p></td>
<td align="left"><p>始终设置为 6，对于 TCP。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>标头的校验和</strong></p></td>
<td align="left"><p>微型端口驱动程序，必须重新计算此字段的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>源地址</strong></p></td>
<td align="left"><p>此字段的值必须是相同的所有合并的段。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标地址</strong></p></td>
<td align="left"><p>此字段的值必须是相同的所有合并的段。</p></td>
</tr>
</tbody>
</table>

 

## <a name="updating-ipv6-header-fields-for-coalesced-segments"></a>正在更新合并的段的 IPv6 标头字段


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>版本</strong></p></td>
<td align="left"><p>此字段的值必须是相同的所有合并的段。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>流量类</strong></p></td>
<td align="left"><p>此字段的值必须是相同的所有合并的段。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>流标签</strong></p></td>
<td align="left"><p>此字段的值必须是相同的所有合并的段。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>有效负载长度</strong></p></td>
<td align="left"><p>每当与 TCP 有效负载长度不为零的新段合并到现有段时，必须重新计算此字段的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>下一标头</strong></p></td>
<td align="left"><p>始终设置为 6，对于 TCP。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>跃点限制</strong></p></td>
<td align="left"><p>必须设置为所需的最低<strong>跃点限制</strong>合并的段的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>源地址</strong></p></td>
<td align="left"><p>此字段的值必须是相同的所有合并的段。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标地址</strong></p></td>
<td align="left"><p>此字段的值必须是相同的所有合并的段。</p></td>
</tr>
</tbody>
</table>

 

 

 





