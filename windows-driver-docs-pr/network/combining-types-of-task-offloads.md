---
title: 组合任务卸载的类型
description: 组合任务卸载的类型
keywords:
- 任务卸载 WDK TCP/IP 传输，组合卸载类型
- 组合任务卸载类型 WDK TCP/IP 卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f467f2e9f722aa0e19c8ab1e06cb8c91aa6d025
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817629"
---
# <a name="combining-types-of-task-offloads"></a>组合任务卸载的类型





以下限制确定了可以在系统上激活的 NDIS 6.0 和更高版本任务卸载服务的组合：

-   支持任务卸载的微型端口适配器仅支持校验和卸载。

-   大量发送卸载版本 1 (LSOV1) 支持的网络接口卡 (NIC) 必须支持 V4 TCP 和 IPv4 校验和传输卸载服务。 如果支持 LSOV1 的微型端口适配器还 (IPsec) 卸载支持 Internet 协议安全，NDIS 会将适配器配置为卸载 IPsec 或 LSOV1，但不能同时用于这两者。

-   大量发送卸载版本 2 (LSOV2) 功能的微型端口适配器必须支持 TCP 和 IP 校验和传输卸载。 如果支持 LSOV2 的微型端口适配器还支持 IPsec 卸载，NDIS 会将其配置为卸载 IPsec 或 LSOV2，但不能同时用于这两者。

无需微型端口驱动程序即可支持 IPv4 和 IPv6。 所有 NDIS 6.0 和更高版本的微型端口驱动程序都必须支持以太网802.3 封装，能够支持以太网 802.1 Q 标记。 下表描述了微型端口驱动程序报告对各种卸载功能的支持时的硬件要求。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">卸载类型</th>
<th align="left">IPv4</th>
<th align="left">IpV6</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>校验和卸载</strong></p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>UDP 校验和</p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>可选</p></td>
</tr>
<tr class="odd">
<td align="left"><p>TCP 校验和</p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>可选</p></td>
</tr>
<tr class="even">
<td align="left"><p>TCP 选项</p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>TCP 校验和) 所需 (</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IP 校验和</p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>不适用</p></td>
</tr>
<tr class="even">
<td align="left"><p>IP 选项</p></td>
<td align="left"><p>TCP 校验和) 所需 (</p></td>
<td align="left"><p>不适用</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IP 扩展标头</p></td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>必需 (128 字节) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>大量发送卸载版本 1 (LSOv1) </strong></p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>最大卸载大小</p></td>
<td align="left"><p>&lt;= 64K</p></td>
<td align="left"><p>不适用</p></td>
</tr>
<tr class="even">
<td align="left"><p>TCP 选项</p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p>不适用</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IP 选项</p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p>不适用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>大型发送卸载版本 2 (LSOv2) </strong></p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>最大卸载大小</p></td>
<td align="left"><p>无限制</p></td>
<td align="left"><p>无限制</p></td>
</tr>
<tr class="even">
<td align="left"><p>IP 选项</p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p>必需 (128 字节) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>IP ID 支持</p></td>
<td align="left"><p>0x0000 到0xffff</p></td>
<td align="left"><p>0x0000 为分段卸载保留0x7fff</p></td>
</tr>
</tbody>
</table>

 

 

 





