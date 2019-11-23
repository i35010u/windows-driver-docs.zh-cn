---
title: OID_SWITCH_NIC_CREATE
description: Hyper-v 可扩展交换机的协议边缘发出 OID_SWITCH_NIC_CREATE 的对象标识符（OID）设置请求，通知底层的可扩展交换机扩展在可扩展交换机端口与之间建立新连接外部或虚拟网络适配器。 完全建立连接后，可扩展交换机的协议边缘发出 OID_SWITCH_NIC_CONNECT 的 OID 设置请求。
ms.assetid: 1D6B2C6B-A63E-4A20-B534-AF12714F5FB5
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_CREATE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1bbb07902faf3d85eefd456f0cd7c814af03a372
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843960"
---
# <a name="oid_switch_nic_create"></a>OID\_交换机\_NIC\_创建


Hyper-v 可扩展交换机的协议边缘发出 OID\_SWITCH\_NIC 的对象标识符（OID）设置请求，\_创建通知底层可扩展交换机扩展在可扩展交换机端口与外部或虚拟网络适配器之间建立了新连接。 完全建立连接后，可扩展交换机的协议边缘会发出 oid [\_switch\_NIC\_连接](oid-switch-nic-connect.md)的 oid 集请求。

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_SWITCH\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构的指针。

<a name="remarks"></a>备注
-------

NDIS\_交换机的**PortId**成员[ **\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构指定为其进行创建通知的可扩展交换机端口。 可扩展交换机扩展可以通过发出 oid [\_switch\_端口\_数组](oid-switch-port-array.md)的 oid 查询请求，获取可扩展交换机上此端口和其他端口的参数信息。

NDIS\_交换机的**索引**成员[ **\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构指定正在为其进行创建通知的网络适配器的索引。 具有指定**索引**值的网络适配器连接到由**PortId**成员指定的可扩展交换机端口。 有关这些索引值的详细信息，请参阅[网络适配器索引值](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)。

当接收到 oid\_SWITCH\_NIC\_创建请求时，扩展必须遵循以下准则：

-   扩展不能修改与 OID 请求关联[ **\_NIC\_参数结构的 NDIS\_开关**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)。

-   OID\_交换机\_NIC\_CREATE 请求仅通知扩展：正在启动新的可扩展交换机连接，并且包流量可能很快就会在指定的端口上发生。 但是，扩展不能使用该端口，直到可扩展交换机的协议边缘发出 oid 的 OID 集请求[\_交换机\_NIC\_连接](oid-switch-nic-connect.md)。 在发出 OID 之前，扩展不能执行以下操作：

    -   为发出 OID\_交换机\_NIC\_CREATE OID 请求的可扩展交换机端口上的网络适配器连接生成任何数据包流量。

    -   转发或发起 oid [\_交换机\_nic\_请求请求发送到请求](oid-switch-nic-request.md)的基础网络\_\_适配器请求。\_

    -   转发或产生 Ndis\_状态的 NDIS 状态指示[ **\_交换机\_nic\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)来自基础网络适配器，该适配器为其发出 OID\_交换机\_NIC\_CREATE OID 请求。

    -   调用[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) ，以在可扩展交换机端口上为指定网络适配器连接递增可扩展交换机引用计数器。

    **请注意**  扩展可能会截获 OID 的 oid 请求之间的指定端口的发送或接收数据包\_交换机\_NIC\_CREATE 和[OID\_nic\_连接](oid-switch-nic-connect.md)。\_ 在这种情况下，扩展应转发发送或接收数据包请求，而不是将其取消。

     

-   扩展可以通过将 NDIS\_状态返回\_数据\_未\_为 OID 请求接受，来否决创建通知。 例如，如果某个扩展无法满足指定端口上的配置策略，则扩展应否决创建通知。

    如果扩展返回其他 NDIS\_状态\_*Xxx*状态代码，则创建通知也被否决。 然而，为暂时性方案返回状态代码（如将 NDIS\_状态返回\_资源）可能会导致创建通知重试。

    如果扩展不否决 OID 请求，则应在请求完成时监视状态。 扩展应执行此操作，以确定可扩展交换机控制路径中的基础扩展或可扩展交换机接口是否否决了 OID 请求。

    **请注意**  扩展**只能在** [**NDIS\_交换机\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构指定网络适配器索引值为零的情况下拒绝 OID 请求。

     

-   如果扩展不否决创建通知，则必须调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)将此 OID 请求转发到可扩展交换机驱动程序堆栈中的基础扩展。

    **请注意**  扩展应监视此 OID 请求的完成状态。 此扩展将执行此命令以检测可扩展交换机驱动程序堆栈中的基础扩展是否否决了创建通知。

     

-   如果扩展调用[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)来转发此 OID 请求，则该扩展将不会立即收到进出可扩展交换机端口的任何数据包流量。 此外，该扩展插件不能立即为可扩展交换机端口注入发送或接收流量。

-   该扩展只能在可扩展交换机的协议边缘发出 oid [\_交换机\_NIC\_连接](oid-switch-nic-connect.md)的 oid 集请求后，将数据包流量转发到可扩展交换机端口。

    **请注意**  在某些情况下，可通过可扩展交换机将数据包流量转发到端口，然后才能通过 OID [\_交换机\_NIC\_连接](oid-switch-nic-connect.md)发出。

     

-   可扩展交换机外部网络适配器可以绑定到一个或多个基础物理适配器。 对于绑定到外部网络适配器的每个物理网络适配器，可扩展交换机的协议边缘将\_NIC\_创建的单独 OID 集请求颁发\_交换机。 每个 OID 集请求指定一个不同的网络适配器连接索引值。 有关这些索引值的详细信息，请参阅[网络适配器索引值](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)。

    扩展必须维护每个基础物理适配器的连接状态。 有关可以将物理网络适配器绑定到外部网络适配器的不同配置的详细信息，请参阅[物理网络适配器配置的类型](https://docs.microsoft.com/windows-hardware/drivers/network/types-of-physical-network-adapter-configurations)。

有关可扩展交换机端口和网络适配器连接状态的详细信息，请参阅[Hyper-v 可扩展交换机端口和网络适配器状态](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)。

**请注意**  扩展不能\_交换机上自行发出 oid 设置请求，\_NIC\_CREATE。

 

### <a name="return-status-codes"></a>返回状态代码

如果扩展\_NIC\_CREATE 完成 oid\_切换，则返回以下状态代码之一。

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
<td><p>NDIS_STATUS_DATA_NOT_ACCEPTED</p></td>
<td><p>该扩展否决了创建通知。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_RESOURCES</p></td>
<td><p>由于资源不足，扩展拒绝了创建通知。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>由于其他原因，扩展拒绝了创建通知。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  扩展是否完成了 OID 设置请求，则不能\_SUCCESS 返回 NDIS\_状态。

 

如果扩展未完成 OID\_交换机\_NIC 的 OID 集请求\_创建，则该请求将由可扩展交换机的基础微型端口边缘完成。 基础微型端口边缘返回此 OID 集请求的以下状态代码：

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
[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[ **\_NIC\_参数的 NDIS\_交换机**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[OID\_交换机\_NIC\_连接](oid-switch-nic-connect.md)

[OID\_交换机\_端口\_数组](oid-switch-port-array.md)

[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)

 

 




