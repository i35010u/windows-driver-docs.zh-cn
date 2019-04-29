---
title: 组合任务卸载的类型
description: 组合任务卸载的类型
ms.assetid: 33f8ba3c-09ab-4041-9641-d4207b98c8b7
keywords:
- 任务卸载，WDK TCP/IP 传输，组合卸载类型
- 组合任务卸载类型 WDK TCP/IP 卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b387f5092c4abfda70725a7e134df39950d7f978
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356924"
---
# <a name="combining-types-of-task-offloads"></a>组合任务卸载的类型





以下限制确定哪种组合的 NDIS 6.0 和更高版本的任务卸载服务可以在系统上处于活动状态：

-   任务支持卸载的微型端口适配器可以支持单独的校验和卸载。

-   大量发送卸载版本 1 (LSOV1) 的功能的网络接口卡 (NIC) 必须支持 V4 TCP 和 IPv4 校验和传输卸载服务。 如果支持 LSOV1 的微型端口适配器还支持的 Internet 协议安全 (IPsec) 卸载，NDIS 将配置要卸载 IPsec 或 LSOV1，但不是两者的适配器。

-   大量发送卸载版本 2 (LSOV2)-支持的微型端口适配器必须支持 TCP 和 IP 校验和传输卸载。 如果 LSOV2 支持的微型端口适配器还支持 IPsec 卸载，NDIS 将将其配置为将 IPsec 或 LSOV2，但不是能同时卸载。

微型端口驱动程序不需要支持 IPv4 和 IPv6。 所有 NDIS 6.0 和更高版本的微型端口驱动程序必须能够都支持以太网 802.1Q 标记都支持以太网 802.3 封装。 下表介绍当微型端口驱动程序报告支持用于各种卸载功能的硬件要求。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">类型的卸载</th>
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
<td align="left"><p>TCP Checksum</p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>可选</p></td>
</tr>
<tr class="even">
<td align="left"><p>TCP 选项</p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>必需 （适用于 TCP 校验和）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IP 校验和</p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>不适用</p></td>
</tr>
<tr class="even">
<td align="left"><p>IP 选项</p></td>
<td align="left"><p>必需 （适用于 TCP 校验和）</p></td>
<td align="left"><p>不适用</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IP 扩展标头</p></td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>必需 （128 个字节）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>大量发送卸载版本 1 (LSOv1)</strong></p></td>
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
<td align="left"><p>必需</p></td>
<td align="left"><p>不适用</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IP 选项</p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p>不适用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>大量发送卸载版本 2 (LSOv2)</strong></p></td>
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
<td align="left"><p>必需</p></td>
<td align="left"><p>必需 （128 个字节）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>IP ID 支持</p></td>
<td align="left"><p>0x0000 到 0xffff 之间</p></td>
<td align="left"><p>0x0000 到 0x7fff 留待分段的卸载</p></td>
</tr>
</tbody>
</table>

 

 

 





