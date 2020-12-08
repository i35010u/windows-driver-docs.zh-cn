---
title: 更新合并段的 IP 标头
description: 本部分介绍如何更新合并段的 IP 标头
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f571167764f9632fcdedf2658a0e684e0b80972a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837903"
---
# <a name="updating-the-ip-headers-for-coalesced-segments"></a>更新合并段的 IP 标头


在 (SCU) 中完成单个合并单元时，接收段会合并 (RSC) 支持的微型端口驱动程序更新 IP 标头中的字段，如下表所述。

-   [正在更新合并段的 IPv4 标头字段](#updating-ipv4-header-fields-for-coalesced-segments)
-   [正在更新合并段的 IPv6 标头字段](#updating-ipv6-header-fields-for-coalesced-segments)

## <a name="updating-ipv4-header-fields-for-coalesced-segments"></a>正在更新合并段的 IPv4 标头字段


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>版本</strong></p></td>
<td align="left"><p>对于所有合并段，此字段的值必须相同。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>标头长度</strong></p></td>
<td align="left"><p>基本 IPv4 标头的长度，没有任何 IP 选项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>差分服务</strong></p></td>
<td align="left"><p>对于所有合并段，此字段的值必须相同。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ECN 位</strong></p></td>
<td align="left"><p>请参阅 <a href="exception-conditions-that-terminate-coalescing.md" data-raw-source="[Exception Conditions that Terminate Coalescing](exception-conditions-that-terminate-coalescing.md)">终止合并的异常情况中的</a>异常8。 如果数据报的 ECN 位的值相同，则应合并它们。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>总长度</strong></p></td>
<td align="left"><p>每次将具有非零 TCP 负载长度的新段合并到现有的 SCU 中时，必须重新计算此字段的值。 有关此字段中的值产生的特殊情况，请参阅 <a href="exception-conditions-that-terminate-coalescing.md" data-raw-source="[Exception Conditions that Terminate Coalescing](exception-conditions-that-terminate-coalescing.md)">终止合并的异常情况</a> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>标识</strong></p></td>
<td align="left"><p>必须设置为第一个合并段的 IP ID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>标记</strong></p></td>
<td align="left"><ul>
<li><p>数据报可以合并，只要它们具有的 DF 值相同 (不分段) 位：全部设置或全部清除。</p></li>
<li><p>具有 MF (多个片段的段不能合并) 位集。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><strong>片段偏移量</strong></p></td>
<td align="left"><p>不适用。 分段 IP 数据报不合并。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>生存时间</strong></p></td>
<td align="left"><p>必须设置为所合并段的最小生存时间 (TTL) 值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>协议</strong></p></td>
<td align="left"><p>对于 TCP，始终设置为6。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>标头校验和</strong></p></td>
<td align="left"><p>此字段的值必须由微型端口驱动程序重新计算。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>源地址</strong></p></td>
<td align="left"><p>对于所有合并段，此字段的值必须相同。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标地址</strong></p></td>
<td align="left"><p>对于所有合并段，此字段的值必须相同。</p></td>
</tr>
</tbody>
</table>

 

## <a name="updating-ipv6-header-fields-for-coalesced-segments"></a>正在更新合并段的 IPv6 标头字段


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>版本</strong></p></td>
<td align="left"><p>对于所有合并段，此字段的值必须相同。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>流量类</strong></p></td>
<td align="left"><p>对于所有合并段，此字段的值必须相同。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>流标签</strong></p></td>
<td align="left"><p>对于所有合并段，此字段的值必须相同。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>负载长度</strong></p></td>
<td align="left"><p>每当具有非零 TCP 负载长度的新段合并到现有段时，必须重新计算此字段的值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>下一标头</strong></p></td>
<td align="left"><p>对于 TCP，始终设置为6。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>跃点限制</strong></p></td>
<td align="left"><p>必须设置为合并段的最小 <strong>跃点限制</strong> 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>源地址</strong></p></td>
<td align="left"><p>对于所有合并段，此字段的值必须相同。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标地址</strong></p></td>
<td align="left"><p>对于所有合并段，此字段的值必须相同。</p></td>
</tr>
</tbody>
</table>

 

 

 





