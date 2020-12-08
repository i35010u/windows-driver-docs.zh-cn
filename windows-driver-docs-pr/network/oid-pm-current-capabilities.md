---
title: OID_PM_CURRENT_CAPABILITIES
description: 作为查询，过量驱动程序可以使用 OID_PM_CURRENT_CAPABILITIES OID 来查询网络适配器当前可用的电源管理功能。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PM_CURRENT_CAPABILITIES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 22868a06cb88802302e80530277e895b285e753a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833319"
---
# <a name="oid_pm_current_capabilities"></a>OID \_ PM \_ 当前 \_ 功能


作为查询，过量驱动程序可以使用 "OID \_ PM \_ 当前 \_ 功能" oid 来查询网络适配器当前可用的电源管理功能。 成功从 OID 查询请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ PM \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构的指针。

<a name="remarks"></a>备注
-------

NDIS 处理微型端口驱动程序的查询。 从 NDIS 6.20 开始，微型端口驱动程序在初始化期间提供电源管理硬件功能。 但是，NDIS 可以隐藏协议驱动程序中的某些功能。 例如，当用户禁用部分或全部电源管理功能时，NDIS 可能会报告不同的功能。

请注意，NDIS 向协议驱动程序报告的当前电源管理功能并不一定与微型端口驱动程序报告给 NDIS 的硬件功能相同。

在绑定操作过程中，NDIS 会报告基础网络适配器的电源管理功能，以覆盖 [**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构 **PowerManagementCapabilitiesEx** 成员中的协议驱动程序。 因此，协议驱动程序不必查询 OID。

NDIS 发出 [**ndis \_ 状态 \_ PM \_ 功能 \_ 更改**](./ndis-status-pm-capabilities-change.md) 状态指示，报告对过量驱动程序可用的电源管理功能的更改。

如果基础网络适配器具有 NDIS 6.1 或更低的微型端口驱动程序，NDIS 会将基础网络适配器的电源管理功能转换为 [**NDIS \_ PM \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities) 结构。

NDIS 为请求返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>NDIS \_ 状态 \_ 成功  
请求已成功完成。 **InformationBuffer** 指向 [**NDIS \_ PM \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构。

<a href="" id="ndis-status-pending"></a>NDIS \_ 状态 \_ 挂起  
请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS \_ 状态 \_ 缓冲区 \_ 太 \_ 短  
信息缓冲区太短。 NDIS 设置 **数据。查询 \_ 信息。** 将 NDIS OID 请求结构中的成员 BytesNeeded \_ \_ 为所需的最小缓冲区大小。

<a href="" id="ndis-status-failure"></a>NDIS \_ 状态 \_ 故障  
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
<td><p>在 NDIS 6.20 和更高版本中受支持。 未请求微型端口驱动程序。 （请参见“备注”部分。）</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ PM \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)

[**NDIS \_ 状态 \_ PM \_ 功能 \_ 更改**](./ndis-status-pm-capabilities-change.md)

 

