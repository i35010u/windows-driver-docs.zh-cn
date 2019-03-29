---
title: MB 微型端口驱动程序类型
description: MB 微型端口驱动程序类型
ms.assetid: ec1743a1-4c5e-4960-b352-40fc5b9c016a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d211d9601932917cd491dcb09c46416161997704
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463821"
---
# <a name="mb-miniport-driver-types"></a>MB 微型端口驱动程序类型


根据数据数据包处理、 DHCP 服务器和 ARP 模拟功能，多个 MB 微型端口驱动程序的实现类型包括可能。 下表显示不同可能的实现类型和生产质量的微型端口驱动程序的所需的实现。

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
<th align="left">ARP 仿真</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>启用了 DHCP 仿真的以太网仿真</p></td>
<td align="left"><p>NdisMedium802_3</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>必需</p></td>
</tr>
<tr class="even">
<td align="left"><p>使用 DHCP 的以太网仿真</p></td>
<td align="left"><p>NdisMedium802_3</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>必需</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IP 数据包处理启用了 DHCP 仿真</p></td>
<td align="left"><p>NdisMediumWirelessWan</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>不必需</p></td>
</tr>
<tr class="even">
<td align="left"><p>IP 数据包处理功能</p></td>
<td align="left"><p>NdisMediumWirelessWan</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>非必需</p></td>
</tr>
</tbody>
</table>

 

在开发或迁移阶段，微型端口驱动程序可以指定任何前三个条目。 但是，生产质量的微型端口驱动程序应使用仅表 （"IP 数据包处理功能"） 的最后一项中指定的设置。

生产质量 MB 微型端口驱动程序应在下表中的 INF 文件中指定的设置。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">INF 文件中的字段</th>
<th align="left">建议的值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>*IfType</p></td>
<td align="left"><p>IF_TYPE_WWANPP / IF_TYPE_WWANPP2</p></td>
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
<td align="left"><p>"flpp4"和"flpp6"（如果支持 IPv6）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LowerRange</p></td>
<td align="left"><p>"ppip"</p></td>
</tr>
</tbody>
</table>

 

 

 





