---
title: 可选电源管理 OID
description: 可选电源管理 OID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d784e0a5a52ac92a392a0043f5ffd73a47f04772
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832125"
---
# <a name="optional-power-management-oids"></a>可选电源管理 OID





要使 NDIS 考虑设备电源管理-感知，必须响应下表中列出的三个电源管理 Oid。 如果设备返回故障状态代码来响应 [OID \_ PNP \_ 功能](./oid-pnp-capabilities.md)的查询，则主机会将设备视为不能进行电源管理。 NDIS 决定是否根据远程 NDIS 设备连接到的基础总线技术来查询此 OID。 某些总线可以对电源进行管理，例如 USB，因此，这些类型的远程 NDIS 设备应该支持将最小 Oid 视为可管理的功能。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">支持</th>
<th align="left">OID</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-pnp-capabilities" data-raw-source="[OID_PNP_CAPABILITIES](./oid-pnp-capabilities.md)">OID_PNP_CAPABILITIES</a></p></td>
<td align="left"><p>NIC 的电源管理功能</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-pnp-query-power" data-raw-source="[OID_PNP_QUERY_POWER](./oid-pnp-query-power.md)">OID_PNP_QUERY_POWER</a></p></td>
<td align="left"><p>用于确定设备是否可以过渡到特定电源状态的查询。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-pnp-set-power" data-raw-source="[OID_PNP_SET_POWER](./oid-pnp-set-power.md)">OID_PNP_SET_POWER</a></p></td>
<td align="left"><p>用于将设备设置为指定电源状态的命令</p></td>
</tr>
</tbody>
</table>

 

