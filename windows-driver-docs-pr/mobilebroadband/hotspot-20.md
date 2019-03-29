---
title: 热点 2.0
description: 热点 2.0
ms.assetid: 4dbd242d-8745-4ab2-b1dc-9f9dd9a73b42
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ba7481b0669a20179ea355c5e0fd9b3726abca3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575681"
---
# <a name="hotspot-20"></a>热点 2.0


热点 2.0 是一种标准到热点的无缝身份验证。 热点 2.0 提供了客户端访问点之间的加密的连接。 它使用 IEEE 802.11u 它在建立连接之前与提供程序通信。 通过使用 WPA2-企业以及几个 EAP 方法之一提供了身份验证和加密。

下表介绍常见热点 2.0 定义的凭据类型：

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>凭据</th>
<th>EAP 方法</th>
<th>支持的 EAP 方法</th>
<th>用户可以输入凭据</th>
<th>运算符可以预配的凭据</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>用户名和密码</p></td>
<td><p>EAP-TTLS</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Certificate</p></td>
<td><p>EAP-TTLS</p></td>
<td><p>是</p></td>
<td><p>是的<em></p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>SIM</p></td>
<td><p>EAP-SIM 或 EAP-AKA</p></td>
<td><p>是</p></td>
<td><p>是</em></p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>

 

\*用户可以从证书中选择或 SIM 已存在于系统上。

Windows 8 和 Windows 8.1 不支持发现或联机注册部分热点 2.0 中，但它们支持 WPA2-企业和所需的热点 2.0 规范的所有 EAP 方法。 因此，Windows 8 和 Windows 8.1 可以连接到热点 2.0 网络时用户已有的凭据。

因为 Windows 8 和 Windows 8.1 不支持 802.11u 发现，运算符必须预配 Windows 8 或 Windows 8.1 与包含其网络适用 Ssid 的无线配置文件。

Windows 10 完全支持热点 2.0 发行版 1，其中包括发现和配置文件创建。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[热点身份验证方法](hotspot-authentication-methods.md)

 

 






