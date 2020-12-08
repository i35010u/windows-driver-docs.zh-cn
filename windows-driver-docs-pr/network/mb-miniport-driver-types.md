---
title: MB 微型端口驱动程序类型
description: MB 微型端口驱动程序类型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 203d5dd1d739fc58e3a03cb480854d9a46efad81
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801605"
---
# <a name="mb-miniport-driver-types"></a>MB 微型端口驱动程序类型


基于数据数据包处理、DHCP 服务器和 ARP 模拟，可以有多个 MB 微型端口驱动程序实现类型。 下表显示了各种可能的实现类型和生产质量微型端口驱动程序所需的实现。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">描述</th>
<th align="left">MediaType</th>
<th align="left">EnableDhcp</th>
<th align="left">ARP 模拟</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>通过 DHCP 仿真进行以太网模拟</p></td>
<td align="left"><p>NdisMedium802_3</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>必须</p></td>
</tr>
<tr class="even">
<td align="left"><p>不带 DHCP 的以太网仿真</p></td>
<td align="left"><p>NdisMedium802_3</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>必须</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IP 数据包处理与 DHCP 仿真</p></td>
<td align="left"><p>NdisMediumWirelessWan</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>不是必需</p></td>
</tr>
<tr class="even">
<td align="left"><p>IP 数据包处理功能</p></td>
<td align="left"><p>NdisMediumWirelessWan</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>不需要</p></td>
</tr>
</tbody>
</table>

 

在开发或迁移阶段，微型端口驱动程序可以指定前三个条目中的任意一个。 但是，生产质量微型端口驱动程序应仅使用在表的最后一项中指定的设置， ( "IP 包处理能力" ) 。

生产质量 MB 微型端口驱动程序应在 INF 文件中指定下表中的设置。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">INF 文件中的字段</th>
<th align="left">建议值 (s) </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>*IfType</p></td>
<td align="left"><p>IF_TYPE_WWANPP/IF_TYPE_WWANPP2</p></td>
</tr>
<tr class="even">
<td align="left"><p>MediaType</p></td>
<td align="left"><p>NdisMediumWirelessWan</p></td>
</tr>
<tr class="odd">
<td align="left"><p>EnableDhcp</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>UpperRange</p></td>
<td align="left"><p>如果支持 IPv6，则为 "flpp4" 和 "flpp6" () </p></td>
</tr>
<tr class="odd">
<td align="left"><p>LowerRange</p></td>
<td align="left"><p>"ppip"</p></td>
</tr>
</tbody>
</table>

 

 

 





