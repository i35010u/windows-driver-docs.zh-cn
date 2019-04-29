---
title: Wi-Fi 热点卸载结构
description: Wi-Fi 热点卸载结构
ms.assetid: 7ec80296-1ac9-48df-a250-6fd856c57901
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49fe098d8f5a42877a01068d91b4fc5d7c39940b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378727"
---
# <a name="wi-fi-hotspot-offloading-structures"></a>Wi-Fi 热点卸载结构

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]

本部分介绍的 Wi-fi 热点卸载框架的数据结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="hotspot-host-handlers.md" data-raw-source="[HOTSPOT_HOST_HANDLERS](hotspot-host-handlers.md)">HOTSPOT_HOST_HANDLERS</a></p></td>
<td><p>此结构包含热点主机处理程序函数表。</p></td>
</tr>
<tr class="even">
<td><p><a href="hotspot-plugin-apis.md" data-raw-source="[HOTSPOT_PLUGIN_APIS](hotspot-plugin-apis.md)">HOTSPOT_PLUGIN_APIS</a></p></td>
<td><p>此结构包含热点插件 Api 函数表。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-connection-context.md" data-raw-source="[HS_CONNECTION_CONTEXT](hs-connection-context.md)">HS_CONNECTION_CONTEXT</a></p></td>
<td><p>此结构包含 post 连接身份验证插件所需的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-device-identity.md" data-raw-source="[HS_DEVICE_IDENTITY](hs-device-identity.md)">HS_DEVICE_IDENTITY</a></p></td>
<td><p>此结构包含有关设备制造商和 phone 模型的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-mac-address.md" data-raw-source="[HS_MAC_ADDRESS](hs-mac-address.md)">HS_MAC_ADDRESS</a></p></td>
<td><p>此结构包含主机媒体访问控制 (MAC) 地址。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-network-identity.md" data-raw-source="[HS_NETWORK_IDENTITY](hs-network-identity.md)">HS_NETWORK_IDENTITY</a></p></td>
<td><p>此结构包含唯一标识的 Wi-fi 网络的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-network-profile.md" data-raw-source="[HS_NETWORK_PROFILE](hs-network-profile.md)">HS_NETWORK_PROFILE</a></p></td>
<td><p>此结构包含所需的连接信息的目标网络。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-plugin-cellular-exception-hosts.md" data-raw-source="[HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS](hs-plugin-cellular-exception-hosts.md)">HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS</a></p></td>
<td><p>此结构包含的主机，该插件必须连接到通过移动电话的持有者的列表。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-plugin-host-name.md" data-raw-source="[HS_PLUGIN_HOST_NAME](hs-plugin-host-name.md)">HS_PLUGIN_HOST_NAME</a></p></td>
<td><p>此结构包含的主机名。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-plugin-profile.md" data-raw-source="[HS_PLUGIN_PROFILE](hs-plugin-profile.md)">HS_PLUGIN_PROFILE</a></p></td>
<td><p>此结构包含有关该插件的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-plugin-supported-sims.md" data-raw-source="[HS_PLUGIN_SUPPORTED_SIMS](hs-plugin-supported-sims.md)">HS_PLUGIN_SUPPORTED_SIMS</a></p></td>
<td><p>此结构包含支持的 SIM 配置的列表。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-plugin-version.md" data-raw-source="[HS_PLUGIN_VERSION](hs-plugin-version.md)">HS_PLUGIN_VERSION</a></p></td>
<td><p>此结构包含该插件所支持的最小值和最大热点主机版本。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-sim-data.md" data-raw-source="[HS_SIM_DATA](hs-sim-data.md)">HS_SIM_DATA</a></p></td>
<td><p>此结构包含标识信息从 SIM 卡获取。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-sim-identity.md" data-raw-source="[HS_SIM_IDENTITY](hs-sim-identity.md)">HS_SIM_IDENTITY</a></p></td>
<td><p>此结构包含 SIM EAP-SIM 或 EAP-AKA 身份验证所需的标识信息。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[卸载引用的 Wi-fi 热点](wi-fi-hotspot-offloading-reference.md)  



