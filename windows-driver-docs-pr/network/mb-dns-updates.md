---
title: MB DNS 更新
description: MB DNS 更新
ms.assetid: be93f0b4-a075-455e-b03c-6d23a2be7b1d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c578e0d4678d7608da10add204ab1c4b8558c67c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378001"
---
# <a name="mb-dns-updates"></a>MB DNS 更新


本主题描述以通知有关 DNS 地址更新 MB 服务的操作。

微型端口驱动程序应设置**名称服务器**注册表项以更新 Windows 有关 DNS 地址更改。 下表描述了相应的注册表项、 预期值和字符串为 IPv4 和 IPv6 网络的示例。 如果微型端口驱动程序仅支持 IPv4 网络，它应设置仅 IPv4 注册表项。 微型端口驱动程序应设置相应的注册表项，它们通知有关媒体的 Windows 通过发送连接事件之前[ **NDIS\_状态\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)通知。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">IPv4 / IPv6</th>
<th align="left">注册表项</th>
<th align="left">ReplTest1</th>
<th align="left">示例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>IPv4</p></td>
<td align="left"><p>HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces\InterfaceGUID\NameServer</p></td>
<td align="left"><p>以空格分隔的 DNS 服务器 IPv4 地址</p></td>
<td align="left"><p>10.20.30.41</p>
<p>10.20.30.40</p></td>
</tr>
<tr class="even">
<td align="left"><p>IPv6</p></td>
<td align="left"><p>HKLM\SYSTEM\CurrentControlSet\Services\Tcpip6\Parameters\Interfaces\InterfaceGUID\NameServer</p></td>
<td align="left"><p>以空格分隔的 DNS 服务器 IPv6 地址</p></td>
<td align="left"><p>2001:4898:7001:f000:1:2:3:4</p>
<p>2001:4898:7001:f000:1:2:3:5</p></td>
</tr>
</tbody>
</table>

 

仅当指定微型端口驱动程序时，才应使用这些操作**EnableDhcp**为等于其 INF 文件中的为零。 也就是说，微型端口驱动程序未实现 DHCP。

有关处理 IP 地址通知的详细信息，请参阅[MB 微型端口驱动程序 IP 地址通知的准则](guidelines-for-mb-miniport-driver-ip-address-notifications.md)。

 

 





