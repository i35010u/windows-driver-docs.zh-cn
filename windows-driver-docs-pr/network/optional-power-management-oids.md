---
title: 可选电源管理 OID
description: 可选电源管理 OID
ms.assetid: 31c8ec45-ecb2-42e2-be4d-2b89fe02a908
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b7b8551028d0531d4815e6bd4160a814547ac42
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366545"
---
# <a name="optional-power-management-oids"></a>可选电源管理 OID





Ndis 要考虑设备电源管理-注意，它必须响应 Oid 下表中列出的三个电源管理。 如果设备的查询响应中返回了失败状态代码[OID\_PNP\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)，则主机将考虑为不符合可管理电源的设备。 NDIS 决定是否查询此 OID 基于远程 NDIS 设备连接到的基础总线技术。 某些总线是可管理电源的如 USB、，因此应将这些类型的远程 NDIS 设备将支持的最小的 Oid 才能被视为可管理电源的。

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
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities" data-raw-source="[OID_PNP_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-capabilities)">OID_PNP_CAPABILITIES</a></p></td>
<td align="left"><p>NIC 的电源管理功能</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-query-power" data-raw-source="[OID_PNP_QUERY_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-query-power)">OID_PNP_QUERY_POWER</a></p></td>
<td align="left"><p>查询以确定设备是否可以转换为特定电源状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power" data-raw-source="[OID_PNP_SET_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)">OID_PNP_SET_POWER</a></p></td>
<td align="left"><p>要将设备设置为指定的电源状态的命令</p></td>
</tr>
</tbody>
</table>

 

 

 





