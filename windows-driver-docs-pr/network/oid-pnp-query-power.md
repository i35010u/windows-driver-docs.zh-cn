---
title: OID_PNP_QUERY_POWER
description: OID_PNP_QUERY_POWER
ms.assetid: 62675042-3339-48de-97bb-58bfa05e1b39
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_QUERY_POWER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 95612f7679bc453462154b3f99de3ee022cbda64
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547236"
---
# <a name="oidpnpquerypower"></a>OID\_PNP\_查询\_电源





OID\_PNP\_查询\_POWER OID 请求微型端口驱动程序，以指示它是否可以转换为低功耗状态中指定其网络适配器*InformationBuffer*。 低功耗状态指定为一个以下 NDIS\_设备\_电源\_状态的值：

<a href="" id="ndisdevicestated1"></a>**NdisDeviceStateD1**  
这将指定 D1 的设备状态。

<a href="" id="ndisdevicestated2"></a>**NdisDeviceStateD2**  
这将指定 D2 的设备状态。

<a href="" id="ndisdevicestated3"></a>**NdisDeviceStateD3**  
这将指定 D3 的设备状态。

OID\_PNP\_查询\_POWER 请求不用于请求到 D0 设备状态的转换。 只会发送 NDIS [OID\_PNP\_设置\_POWER](oid-pnp-set-power.md)指定 D0 的设备状态的请求。

通过返回 NDIS\_状态\_此 OID 的成功请求，微型端口驱动程序可保证它将转换到指定的设备电源状态，在后续 OID 收到的网络适配器\_PNP\_设置\_POWER 请求。 微型端口驱动程序，在这种情况下，必须执行任何操作危害到太空船转换。

微型端口驱动程序必须始终返回 NDIS\_状态\_到此 OID 请求成功。 任何其他返回代码是错误的。

OID\_PNP\_查询\_电源请求始终后跟 OID\_PNP\_设置\_POWER 请求。 OID\_PNP\_设置\_电源请求可能紧跟 OID\_PNP\_查询\_POWER 请求或可能会到达未指定时间间隔后 OID\_PNP\_查询\_POWER 请求。 D0 OID 中指定的设备状态\_PNP\_设置\_电源请求有效地取消 OID\_PNP\_查询\_POWER 请求。

中间的驱动程序必须始终返回 NDIS\_状态\_OID 的查询的成功\_PNP\_查询\_电源。 中间的驱动程序应永远不会传播 OID\_PNP\_查询\_POWER 请求为基础的微型端口驱动程序。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>NDIS 5.1 和 NDIS 6.0 及更高版本支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

 

 




