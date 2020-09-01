---
title: OID_SWITCH_NIC_CREATE
description: Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID_SWITCH_NIC_CREATE 请求，通知底层可扩展交换机扩展在可扩展交换机端口与外部或虚拟网络适配器之间建立了新连接。 完全建立连接后，可扩展交换机的协议边缘发出 OID_SWITCH_NIC_CONNECT 的 OID 设置请求。
ms.assetid: 1D6B2C6B-A63E-4A20-B534-AF12714F5FB5
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_CREATE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a23c3965498764d1357294dce0cf4fa6760509b5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218361"
---
# <a name="oid_switch_nic_create"></a>OID \_ 交换机 \_ NIC \_ 创建


Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID \_ 交换机 NIC CREATE 的请求， \_ \_ 通知底层可扩展交换机扩展在可扩展交换机端口与外部或虚拟网络适配器之间建立了新连接。 完全建立连接后，可扩展交换机的协议边缘会发出 oid [ \_ 交换机 \_ NIC \_ CONNECT](oid-switch-nic-connect.md)的 oid 设置请求。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构的指针。

<a name="remarks"></a>备注
-------

[**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构的**PortId**成员指定为其进行创建通知的可扩展交换机端口。 可扩展交换机扩展可以通过发出 oid [ \_ 交换机 \_ 端口 \_ 数组](oid-switch-port-array.md)的 oid 查询请求，获取可扩展交换机上此端口和其他端口的参数信息。

[**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构的**index**成员指定为其进行创建通知的网络适配器的索引。 具有指定 **索引** 值的网络适配器连接到由 **PortId** 成员指定的可扩展交换机端口。 有关这些索引值的详细信息，请参阅 [网络适配器索引值](./network-adapter-index-values.md)。

当其收到 oid 交换机 NIC CREATE 的 OID 集请求时 \_ \_ \_ ，扩展必须遵循以下准则：

-   扩展不得修改与 OID 请求关联的 [**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters) 结构。

-   OID \_ 交换机 \_ NIC \_ CREATE 请求仅通知扩展：正在启动新的可扩展交换机连接，并且包流量很快就会在指定的端口上发生。 但是，在可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ NIC \_ CONNECT](oid-switch-nic-connect.md)的 oid 集请求之前，扩展不能使用该端口。 在发出 OID 之前，扩展不能执行以下操作：

    -   为 \_ 发出 oid 交换机 \_ NIC CREATE oid 请求的可扩展交换机端口上的网络适配器连接生成任何数据包流量 \_ 。

    -   向对其发出 OID 交换机 nic CREATE OID 请求的基础网络适配器转发或发起 oid [ \_ 交换器 \_ NIC \_ 请求](oid-switch-nic-request.md) 的 oid 请求 \_ \_ \_ 。

    -   从为其发出 OID 交换机 nic CREATE OID 请求的基础网络适配器转发或产生 ndis 状态 [** \_ \_ 切换 \_ NIC \_ 状态**](./ndis-status-switch-nic-status.md) 的 ndis 状态指示 \_ \_ \_ 。

    -   调用 [*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) ，以在可扩展交换机端口上为指定网络适配器连接递增可扩展交换机引用计数器。

    **注意**   该扩展可能会截获 OID \_ 交换机 \_ nic \_ CREATE 和[oid \_ 交换机 \_ nic \_ CONNECT](oid-switch-nic-connect.md)的 oid 请求之间指定端口的发送或接收数据包。 在这种情况下，扩展应转发发送或接收数据包请求，而不是将其取消。

     

-   此扩展可以通过返回 \_ \_ \_ OID 请求不接受的 NDIS 状态数据来否决创建通知 \_ 。 例如，如果某个扩展无法满足指定端口上的配置策略，则扩展应否决创建通知。

    如果该扩展插件返回其他 NDIS \_ 状态 \_ *Xxx*状态代码，则创建通知也被否决。 然而，为暂时性方案返回状态代码（例如返回 NDIS \_ 状态 \_ 资源）可能会导致创建通知重试。

    如果扩展不否决 OID 请求，则应在请求完成时监视状态。 扩展应执行此操作，以确定可扩展交换机控制路径中的基础扩展或可扩展交换机接口是否否决了 OID 请求。

    **注意**   如果[**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构的**索引**成员指定的网络适配器索引值为零，则扩展只能否决 OID 请求。

     

-   如果扩展不否决创建通知，则必须调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 将此 OID 请求转发到可扩展交换机驱动程序堆栈中的基础扩展。

    **注意**   扩展应监视此 OID 请求的完成状态。 此扩展将执行此命令以检测可扩展交换机驱动程序堆栈中的基础扩展是否否决了创建通知。

     

-   如果扩展调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 来转发此 OID 请求，则该扩展将不会立即收到进出可扩展交换机端口的任何数据包流量。 此外，该扩展插件不能立即为可扩展交换机端口注入发送或接收流量。

-   此扩展只能在可扩展交换机的协议边缘发出 [oid \_ 交换机 \_ NIC \_ CONNECT](oid-switch-nic-connect.md)的 oid 集请求后，将数据包流量转发到可扩展交换机端口。

    **注意**   在某些情况下，在发出 oid [ \_ 交换机 \_ NIC \_ CONNECT](oid-switch-nic-connect.md)的 oid 设置请求之前，可通过可扩展交换机将数据包流量转发到端口。

     

-   可扩展交换机外部网络适配器可以绑定到一个或多个基础物理适配器。 对于绑定到外部网络适配器的每个物理网络适配器，可扩展交换机的协议边缘会发出单独的 OID \_ 交换机 \_ NIC \_ CREATE 请求。 每个 OID 集请求指定一个不同的网络适配器连接索引值。 有关这些索引值的详细信息，请参阅 [网络适配器索引值](./network-adapter-index-values.md)。

    扩展必须维护每个基础物理适配器的连接状态。 有关可以将物理网络适配器绑定到外部网络适配器的不同配置的详细信息，请参阅 [物理网络适配器配置的类型](./types-of-physical-network-adapter-configurations.md)。

有关可扩展交换机端口和网络适配器连接状态的详细信息，请参阅 [Hyper-v 可扩展交换机端口和网络适配器状态](./hyper-v-extensible-switch-port-and-network-adapter-states.md)。

**注意**   扩展不能发出自己的 OID 设置 OID \_ 交换机 \_ NIC CREATE 的请求 \_ 。

 

### <a name="return-status-codes"></a>返回状态代码

如果扩展完成 oid 交换机 NIC CREATE 的 OID 设置 \_ 请求 \_ \_ ，它将返回以下状态代码之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>说明</th>
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

 

**注意**   如果扩展完成了 OID 设置请求，则它不能返回 NDIS \_ 状态 " \_ 成功"。

 

如果扩展未完成 OID 交换机 NIC CREATE 的 OID 集请求 \_ \_ \_ ，则该请求将由可扩展交换机的基础微型端口边缘完成。 基础微型端口边缘返回此 OID 集请求的以下状态代码：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>说明</th>
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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)

[**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[OID \_ 交换机 \_ NIC \_ 连接](oid-switch-nic-connect.md)

[OID \_ 交换机 \_ 端口 \_ 数组](oid-switch-port-array.md)

[*ReferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)

 

