---
title: OID_SWITCH_PORT_TEARDOWN
description: Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID_SWITCH_PORT_TEARDOWN 请求，以通知底层可扩展交换机扩展，可扩展交换机端口将开始删除过程。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_TEARDOWN 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: edd165a9a4926ae61bcb49e0e2a52aeed1980804
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248795"
---
# <a name="oid_switch_port_teardown"></a>OID \_ 交换机 \_ 端口 \_ 拆卸


Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID \_ 交换机 \_ 端口 \_ 拆卸请求，通知底层的可扩展交换机扩展，可扩展交换机端口会开始删除过程。 此过程在协议驱动程序发出 oid [ \_ 交换机 \_ 端口 \_ 删除](oid-switch-port-delete.md)请求时启动。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构的指针。

<a name="remarks"></a>备注
-------

[**NDIS \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构的 **PortId** 成员指定为其发出连接通知的可扩展交换机端口。 可扩展交换机扩展必须按以下方式更新有关其获取的端口的任何缓存信息：

-   发出 oid [ \_ 交换机 \_ 端口 \_ 数组](oid-switch-port-array.md)的 oid 查询请求。 仅当 [OID \_ 开关 \_ 参数](oid-switch-parameters.md)返回将 **IsActive** 设置为 TRUE 的 [**NDIS \_ 开关 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_parameters)结构时，扩展才会在 [*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)上发出此 OID。 如果 **IsActive** 为 FALSE，则扩展小型端口发出 **NetEventSwitchActivate** [**NET \_ PNP \_ 事件**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event) 时，扩展会发出 OID。

-   检查各种 OID 会设置 [oid \_ 交换机 \_ 端口 \_ 创建](oid-switch-port-create.md) 和 [oid \_ 交换机 \_ 端口 \_ 删除](oid-switch-port-delete.md)请求。

可扩展交换机的协议边缘发出 oid 交换机端口拆卸的 OID 集请求 \_ \_ \_ ，通知扩展端口正在从可扩展交换机中删除。 在发出此 OID 请求之前，如果该端口具有活动的网络适配器连接，则可扩展交换机的协议边缘以前颁发了以下 Oid：

-   [OID \_交换机 \_ NIC \_ 断开连接](oid-switch-nic-disconnect.md)，这会通知底层扩展网络适配器不再连接到 [**NDIS \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters) 结构中指定的端口。

-   [OID \_切换 \_ NIC \_ DELETE](oid-switch-nic-delete.md)，这会通知基础扩展网络适配器与可扩展交换机端口之间的网络连接已删除。

    协议边缘在已取消或完成指定的可扩展交换机端口的所有挂起数据包后发出此 OID 集请求。

扩展完成此 OID 集请求并且可扩展交换机端口的引用计数器为零后，可扩展交换机的协议边缘将发出 oid [ \_ 交换机 \_ 端口 \_ 删除](oid-switch-port-delete.md)的 oid 设置请求。 此 OID 请求从可扩展交换机中删除端口。

**注意**  扩展通过调用 [*ReferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)来递增可扩展交换机端口的引用计数器。 扩展通过调用 [*DereferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port)来递减引用计数器。

 

扩展必须遵循以下准则来处理 OID \_ 交换机端口拆卸的 oid 集 \_ 请求 \_ ：

-   扩展必须始终将此 OID 集请求转发到基础扩展。 此扩展不能导致请求失败。

    **注意**  扩展不得修改与 OID 请求关联的 [**NDIS \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters) 结构。

     

-   扩展转发此 OID 请求后，它无法将数据包转发到删除的端口。 扩展还不能为已删除的端口发出 OID 请求，也不能调用 [*ReferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port) 函数。

**注意**  扩展不得颁发 oid \_ 交换机端口拆卸的 oid 设置请求 \_ \_ 。

 

有关可扩展交换机端口和网络适配器连接状态的详细信息，请参阅 [Hyper-v 可扩展交换机端口和网络适配器状态](./hyper-v-extensible-switch-port-and-network-adapter-states.md)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘完成 OID 交换机端口拆卸的 OID 设置 \_ 请求 \_ \_ ，并返回以下状态代码。

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
[*DereferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port)

[*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS \_ 开关 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_parameters)

[**NDIS \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)

[**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[**NET \_ PNP \_ 事件**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)

[OID \_ 交换机 \_ NIC \_ 删除](oid-switch-nic-delete.md)

[OID \_ 开关 \_ 参数](oid-switch-parameters.md)

[OID \_ 交换机 \_ 端口 \_ 数组](oid-switch-port-array.md)

[*ReferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)

 

