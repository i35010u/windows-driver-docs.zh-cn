---
title: OID_SWITCH_NIC_CONNECT
description: Hyper-v 可扩展交换机的协议边缘发出 OID_SWITCH_NIC_CONNECT 的对象标识符（OID）设置请求，通知底层可扩展交换机端口与网络适配器之间的网络连接完全建立。 协议边缘以前通知的扩展，此连接在发出 OID_SWITCH_NIC_CREATE 的 OID 集请求时正在建立。
ms.assetid: 98A4AD28-2716-40DD-AE46-70969A23FAB7
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_CONNECT 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fda275d602e5de033400735e8079c9c8d9692002
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843961"
---
# <a name="oid_switch_nic_connect"></a>OID\_交换机\_NIC\_连接


Hyper-v 可扩展交换机的协议边缘发出\_交换机\_NIC 的对象标识符（OID）设置请求，\_"连接"，通知底层可扩展交换机端口与网络适配器之间的网络连接是完全建立的。 协议边缘以前通知了此连接在其发出 OID [\_SWITCH\_NIC\_CREATE](oid-switch-nic-create.md)的 oid 集请求时所建立的扩展。

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_SWITCH\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构的指针。

<a name="remarks"></a>备注
-------

NDIS\_交换机的**PortId**成员[ **\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构指定为其发出连接通知的可扩展交换机端口。 可扩展交换机扩展可通过以下方式获取此端口和其他可扩展交换机端口的参数信息：

-   通过发出[oid\_SWITCH\_端口\_数组](oid-switch-port-array.md)的 oid 查询请求。 此扩展仅在以下情况下在[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)上发出此 OID： OID\_SWITCH\_参数返回[ **\_\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_parameters)结构，并将**IsActive**设置为 TRUE。 如果**IsActive**为 FALSE，则当扩展微型端口适配器发出**NETEVENTSWITCHACTIVATE** [**NET\_PNP\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)时，扩展将发出 OID。

-   通过检查各种 OID， [\_switch\_端口\_CREATE](oid-switch-port-create.md)和[OID\_SWITCH\_\_删除](oid-switch-port-delete.md)。

NDIS\_交换机的**索引**成员[ **\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构指定正在为其发出连接通知的网络适配器的索引。 具有指定**索引**值的网络适配器连接到由**PortId**成员指定的可扩展交换机端口。 有关这些索引值的详细信息，请参阅[网络适配器索引值](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)。

当接收到 oid\_SWITCH\_NIC\_连接时，扩展必须遵循以下准则：

-   当 OID\_交换机\_NIC\_连接请求完成时，NDIS\_状态\_成功，则网络连接和可扩展交换机端口都是完全正常运行。 此扩展可以生成数据包流量并将数据包转发到端口的网络连接。 扩展还可以颁发可扩展交换机 Oid，或使用端口作为源端口的状态指示。 扩展还可以调用[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)来递增端口的可扩展交换机引用计数器。

-   扩展不能修改与 OID 请求关联[ **\_NIC\_参数结构的 NDIS\_开关**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)。

-   扩展必须始终调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) ，以将此 OID 请求转发到基础扩展。 扩展不能完成 OID 请求本身。

-   可扩展交换机外部网络适配器可以绑定到一个或多个基础物理适配器。 对于绑定到外部网络适配器的每个物理网络适配器，可扩展交换机的协议边缘\_NIC\_连接时发出\_交换机的单独 OID 集请求。 每个 OID 集请求指定一个不同的网络适配器连接索引值。 有关这些值的详细信息，请参阅[网络适配器索引值](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)。

    扩展必须为绑定到外部网络适配器的每个基础物理适配器维护连接状态。 有关可以将物理网络适配器绑定到外部网络适配器的不同配置的详细信息，请参阅[物理网络适配器配置的类型](https://docs.microsoft.com/windows-hardware/drivers/network/types-of-physical-network-adapter-configurations)。

**请注意**  扩展不能\_交换机上自行发出 oid 设置请求，\_NIC\_CONNECT。

 

有关可扩展交换机端口和网络适配器连接状态的详细信息，请参阅[Hyper-v 可扩展交换机端口和网络适配器状态](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘完成 OID\_SWITCH\_NIC 的 OID 集请求\_连接并返回以下状态代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>OID 请求已成功完成。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[ **\_NIC\_参数的 NDIS\_交换机**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[OID\_交换机\_NIC\_创建](oid-switch-nic-create.md)

[OID\_交换机\_端口\_数组](oid-switch-port-array.md)

[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)

 

 




