---
title: OID_SWITCH_NIC_CONNECT
description: Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID_SWITCH_NIC_CONNECT 请求，通知底层可扩展交换机端口与网络适配器之间的网络连接是完全建立的。 协议边缘以前通知的扩展，此连接在发出 OID_SWITCH_NIC_CREATE 的 OID 集请求时正在建立。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_CONNECT 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4c5c07fd196564d6d04d1df954d001b5be317efb
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102247929"
---
# <a name="oid_switch_nic_connect"></a>OID \_ 交换机 \_ NIC \_ 连接


Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID \_ 交换机 \_ NIC CONNECT 的请求 \_ ，通知底层可扩展交换机端口与网络适配器之间的网络连接是完全建立的。 协议边缘以前通知的扩展，此连接在发出 oid [ \_ 交换机 \_ NIC \_ CREATE](oid-switch-nic-create.md)的 oid 集请求时正在建立。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构的指针。

<a name="remarks"></a>备注
-------

[**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构的 **PortId** 成员指定为其发出连接通知的可扩展交换机端口。 可扩展交换机扩展可通过以下方式获取此端口和其他可扩展交换机端口的参数信息：

-   发出 oid [ \_ 交换机 \_ 端口 \_ 数组](oid-switch-port-array.md)的 oid 查询请求。 仅当 OID [](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach) \_ 开关 \_ 参数返回将 **IsActive** 设置为 TRUE 的 [**NDIS \_ 开关 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_parameters)结构时，扩展才会在 FilterAttach 上发出此 OID。 如果 **IsActive** 为 FALSE，则扩展微型端口适配器发出 **NetEventSwitchActivate** [**NET \_ PNP \_ 事件**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event) 时，扩展会发出 OID。

-   检查各种 OID 会设置 [oid \_ 交换机 \_ 端口 \_ 创建](oid-switch-port-create.md) 和 [oid \_ 交换机 \_ 端口 \_ 删除](oid-switch-port-delete.md)请求。

[**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构的 **index** 成员指定正在为其发出连接通知的网络适配器的索引。 具有指定 **索引** 值的网络适配器连接到由 **PortId** 成员指定的可扩展交换机端口。 有关这些索引值的详细信息，请参阅 [网络适配器索引值](./network-adapter-index-values.md)。

当它收到 oid 交换机 NIC CONNECT 的 OID 设置请求时 \_ \_ \_ ，扩展必须遵循以下准则：

-   当 OID \_ 交换机 \_ NIC \_ CONNECT 请求在 NDIS 状态成功完成时 \_ \_ ，网络连接和可扩展交换机端口都将完全正常运行。 此扩展可以生成数据包流量并将数据包转发到端口的网络连接。 扩展还可以颁发可扩展交换机 Oid，或使用端口作为源端口的状态指示。 扩展还可以调用 [*ReferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port) 来递增端口的可扩展交换机引用计数器。

-   扩展不得修改与 OID 请求关联的 [**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters) 结构。

-   扩展必须始终调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) ，以将此 OID 请求转发到基础扩展。 扩展不能完成 OID 请求本身。

-   可扩展交换机外部网络适配器可以绑定到一个或多个基础物理适配器。 对于绑定到外部网络适配器的每个物理网络适配器，可扩展交换机的协议边缘会发出单独的 OID \_ 交换机 \_ NIC \_ CONNECT 请求。 每个 OID 集请求指定一个不同的网络适配器连接索引值。 有关这些值的详细信息，请参阅 [网络适配器索引值](./network-adapter-index-values.md)。

    扩展必须为绑定到外部网络适配器的每个基础物理适配器维护连接状态。 有关可以将物理网络适配器绑定到外部网络适配器的不同配置的详细信息，请参阅 [物理网络适配器配置的类型](./types-of-physical-network-adapter-configurations.md)。

**注意**  扩展不能发出自己的 OID set \_ \_ NIC \_ CONNECT 请求。

 

有关可扩展交换机端口和网络适配器连接状态的详细信息，请参阅 [Hyper-v 可扩展交换机端口和网络适配器状态](./hyper-v-extensible-switch-port-and-network-adapter-states.md)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘完成 OID 交换机 NIC CONNECT 的 OID 设置 \_ 请求 \_ \_ ，并返回以下状态代码。

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
<td><p>Version</p></td>
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标题</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NdisFReturnNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)

[**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[OID \_ 交换机 \_ NIC \_ 创建](oid-switch-nic-create.md)

[OID \_ 交换机 \_ 端口 \_ 数组](oid-switch-port-array.md)

[*ReferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)

 

