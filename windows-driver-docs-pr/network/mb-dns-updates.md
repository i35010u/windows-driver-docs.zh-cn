---
title: MB DNS 更新
description: MB DNS 更新
ms.assetid: be93f0b4-a075-455e-b03c-6d23a2be7b1d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d409d2e4f1024885b64c08ee1257f0b1383f0e8
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207495"
---
# <a name="mb-dns-updates"></a>MB DNS 更新


本主题介绍用于通知 MB 服务有关 DNS 地址更新的操作。

微型端口驱动程序应设置 **NameServer** 注册表项，以更新有关 DNS 地址更改的 Windows。 下表描述了相应的注册表项、预期值和 IPv4 和 IPv6 网络的示例字符串。 如果微型端口驱动程序仅支持 IPv4 网络，则它应仅设置 IPv4 注册表项。 小型端口驱动程序应在通过发送 [**NDIS \_ 状态 \_ 链接 \_ 状态**](./ndis-status-link-state.md) 通知来通知 Windows 媒体连接事件之前，将相应的注册表项设置 () 。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">IPv4/IPv6</th>
<th align="left">注册表项</th>
<th align="left">值</th>
<th align="left">示例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IPv4</p></td>
<td align="left"><p>HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces\InterfaceGUID\NameServer</p></td>
<td align="left"><p>空格分隔的 DNS 服务器 IPv4 地址</p></td>
<td align="left"><p>10.20.30.41</p>
<p>10.20.30.40</p></td>
</tr>
<tr class="even">
<td align="left"><p>IPv6</p></td>
<td align="left"><p>HKLM\SYSTEM\CurrentControlSet\Services\Tcpip6\Parameters\Interfaces\InterfaceGUID\NameServer</p></td>
<td align="left"><p>空格分隔的 DNS 服务器 IPv6 地址</p></td>
<td align="left"><p>2001：4898：7001： f000：1：2：3：4</p>
<p>2001：4898：7001： f000：1：2：3：5</p></td>
</tr>
</tbody>
</table>

 

仅当微型端口驱动程序在其 INF 文件中指定 **EnableDhcp** 等于零时，才应使用这些操作。 也就是说，微型端口驱动程序不实现 DHCP。

有关处理 IP 地址通知的详细信息，请参阅 [用于 MB 微型端口驱动程序 IP 地址通知的准则](guidelines-for-mb-miniport-driver-ip-address-notifications.md)。

 

