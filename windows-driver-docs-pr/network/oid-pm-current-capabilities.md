---
title: OID_PM_CURRENT_CAPABILITIES
description: 作为查询，过量驱动程序可以使用 OID_PM_CURRENT_CAPABILITIES OID 来查询网络适配器当前可用的电源管理功能。
ms.assetid: b35ce325-a1aa-43e0-bf68-cb2ab89dff76
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PM_CURRENT_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c3230d7dc3de542da18d7948b3ad54ca716159ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844060"
---
# <a name="oid_pm_current_capabilities"></a>\_PM\_当前\_功能的 OID


作为查询，过量驱动程序可以使用 OID\_PM\_当前\_功能 OID 来查询网络适配器当前可用的电源管理功能。 成功从 OID 查询请求返回后， [**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构的指针。

<a name="remarks"></a>备注
-------

NDIS 处理微型端口驱动程序的查询。 从 NDIS 6.20 开始，微型端口驱动程序在初始化期间提供电源管理硬件功能。 但是，NDIS 可以隐藏协议驱动程序中的某些功能。 例如，当用户禁用部分或全部电源管理功能时，NDIS 可能会报告不同的功能。

请注意，NDIS 向协议驱动程序报告的当前电源管理功能并不一定与微型端口驱动程序报告给 NDIS 的硬件功能相同。

NDIS 在绑定操作过程中，在[**ndis\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构的**PowerManagementCapabilitiesEx**成员中报告基础网络适配器的电源管理功能. 因此，协议驱动程序不必查询 OID。

NDIS [ **\_状态\_\_PM 发出 ndis 状态\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-capabilities-change)状态指示，以报告适用于过量驱动程序的电源管理功能中的更改。

如果基础网络适配器具有 NDIS 6.1 或更低的微型端口驱动程序，NDIS 会将基础网络适配器的电源管理功能转换为[**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构。

NDIS 为请求返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>成功的 NDIS\_状态\_  
请求已成功完成。 **InformationBuffer**指向[**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_挂起  
请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_状态\_缓存\_\_太短  
信息缓冲区太短。 NDIS 设置**数据。查询\_信息。** \_OID 中的 BytesNeeded 成员\_请求结构到所需的最小缓冲区大小。

<a href="" id="ndis-status-failure"></a>\_故障时的 NDIS\_状态  
由于上述原因之外的原因，导致请求失败。

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
<td><p>在 NDIS 6.20 和更高版本中受支持。 未请求微型端口驱动程序。 （请参见 "备注" 部分。）</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[ **\_绑定\_参数的 NDIS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)

[**NDIS\_状态\_PM\_功能\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-capabilities-change)

 

 




