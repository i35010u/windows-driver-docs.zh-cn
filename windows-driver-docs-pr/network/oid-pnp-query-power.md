---
title: OID_PNP_QUERY_POWER
description: OID_PNP_QUERY_POWER
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_QUERY_POWER 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1af5c5486e92827749cff442cc3de944e041e917
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827537"
---
# <a name="oid_pnp_query_power"></a>OID \_ PNP \_ 查询 \_ 能力





OID \_ PNP \_ 查询 \_ 电源 oid 请求微型端口驱动程序，以指示它是否可以将其网络适配器转换为 *InformationBuffer* 中指定的低功耗状态。 低功耗状态指定为下列 NDIS \_ 设备 \_ 电源 \_ 状态值之一：

<a href="" id="ndisdevicestated1"></a>**NdisDeviceStateD1**  
这会指定设备状态 D1。

<a href="" id="ndisdevicestated2"></a>**NdisDeviceStateD2**  
这会指定设备状态 D2。

<a href="" id="ndisdevicestated3"></a>**NdisDeviceStateD3**  
这将指定 D3 的设备状态。

OID \_ PNP \_ 查询 \_ 电源请求不用于请求转换为 D0 的设备状态。 NDIS 只发送 [OID \_ PNP 集 \_ 的 \_ 电源](oid-pnp-set-power.md) 请求，该请求指定设备状态为 D0。

通过将 NDIS \_ 状态 \_ 成功返回到此 OID 请求，微型端口驱动程序可保证在收到后续 OID \_ PNP \_ 设置电源请求时，它会将网络适配器转换为指定的设备电源状态 \_ 。 在这种情况下，微型端口驱动程序必须不执行任何操作来危害转换。

小型端口驱动程序必须始终 \_ 将 NDIS 状态 \_ 成功返回到此 OID 请求。 任何其他返回代码均为错误。

OID \_ pnp \_ 查询 \_ 电源请求始终后跟 oid \_ pnp \_ 设置 \_ 电源请求。 OID pnp \_ \_ 设置 \_ 电源请求可能会立即遵循 oid pnp \_ 查询电源请求， \_ \_ 或者可能会在 oid \_ pnp \_ 查询电源请求后的指定间隔内到达 \_ 。 OID pnp 设置电源请求中指定的 D0 的设备状态会 \_ \_ \_ 有效地取消 oid \_ pnp \_ 查询 \_ 电源请求。

中间驱动程序必须始终将 NDIS \_ 状态 \_ 成功返回到 OID \_ PNP \_ 查询电源的查询 \_ 。 中间驱动程序绝不应将 OID \_ PNP \_ 查询 \_ 电源请求传播到基础微型端口驱动程序。

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
<td><p>支持 NDIS 5.1 和 NDIS 6.0 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

 

 




