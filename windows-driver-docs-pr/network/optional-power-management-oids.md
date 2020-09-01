---
title: 可选电源管理 OID
description: 可选电源管理 OID
ms.assetid: 31c8ec45-ecb2-42e2-be4d-2b89fe02a908
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38f841a78238971124db34048f29145fc2fd9f29
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206291"
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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities" data-raw-source="[OID_PNP_CAPABILITIES](./oid-pnp-capabilities.md)">OID_PNP_CAPABILITIES</a></p></td>
<td align="left"><p>NIC 的电源管理功能</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-query-power" data-raw-source="[OID_PNP_QUERY_POWER](./oid-pnp-query-power.md)">OID_PNP_QUERY_POWER</a></p></td>
<td align="left"><p>用于确定设备是否可以过渡到特定电源状态的查询。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power" data-raw-source="[OID_PNP_SET_POWER](./oid-pnp-set-power.md)">OID_PNP_SET_POWER</a></p></td>
<td align="left"><p>用于将设备设置为指定电源状态的命令</p></td>
</tr>
</tbody>
</table>

 

 

