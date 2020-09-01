---
title: OID_SWITCH_PORT_DELETE
description: Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID_SWITCH_PORT_DELETE 请求，通知有关如何删除可扩展交换机端口的可扩展交换机扩展。
ms.assetid: D8893395-3D33-4777-B8F0-4DD6BE9B8A37
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_DELETE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fb89e8da1b0bc514110c7e79a462e3f74f266ae6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212121"
---
# <a name="oid_switch_port_delete"></a>\_删除 OID 交换机 \_ 端口 \_


Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID \_ 交换机 \_ 端口 DELETE 的请求 \_ ，通知有关如何删除可扩展交换机端口的可扩展交换机扩展。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构的指针。

<a name="remarks"></a>备注
-------

[**NDIS \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构的**PortId**成员指定为其发出删除通知的可扩展交换机端口。

如果网络适配器连接到指定的端口，则可扩展交换机的协议边缘将在删除该端口之前删除该连接。 在这种情况下，协议边缘将在删除端口之前执行以下步骤：

-   协议边缘发出 oid [ \_ 交换机 \_ NIC \_ 断开连接](oid-switch-nic-disconnect.md) 的 oid 集请求，通知扩展网络适配器与可扩展交换机端口之间的连接正在被删除。

-   在已取消或完成指定的可扩展交换机端口的所有挂起数据包后，协议边缘会发出 oid [ \_ 交换机 \_ NIC \_ DELETE](oid-switch-nic-delete.md) 的 oid 设置请求，通知扩展网络适配器与可扩展交换机端口之间的连接已被删除。

    此时，协议边缘可以开始删除该端口。

可扩展交换机的协议边缘在删除可扩展交换机端口时遵循以下步骤：

1.  可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ 端口 \_ 拆卸](oid-switch-port-teardown.md)的 oid 集请求。 此 OID 请求通知底层的可扩展交换机扩展，了解有关可扩展交换机端口的删除过程的开始。

2.  在 \_ \_ \_ 对可扩展交换机端口的所有 OID 请求都完成之后，协议边缘会发出 oid 交换机端口删除的 oid 设置请求。

    **注意**   如果扩展以前调用了[*ReferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)来递增端口的引用计数器，则必须在协议边缘发出[OID \_ 交换机 \_ NIC \_ DELETE](oid-switch-nic-delete.md)请求之前调用[*DereferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port) 。

     

扩展必须遵循以下准则来处理 OID \_ 交换机端口删除的 oid 集 \_ 请求 \_ ：

-   扩展不得修改与 OID 请求关联的 [**NDIS \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters) 结构。

-   扩展必须始终将此 OID 集请求转发到基础扩展。 此扩展不能导致请求失败。

-   在 OID \_ 交换机 \_ 端口 \_ 删除请求完成并且 NDIS 状态为 "成功" 后 \_ \_ ，该扩展将不会接收已删除端口的任何数据包或 OID 请求。 此扩展无法将数据包转发到已删除的端口。 扩展还不能为已删除的端口发出 OID 请求，也不能调用 [*ReferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port) 函数。

**注意**   可扩展交换机扩展不得颁发 oid \_ 交换机端口删除的 oid 设置 \_ 请求 \_ 。

 

有关可扩展交换机端口和网络适配器连接状态的详细信息，请参阅 [Hyper-v 可扩展交换机端口和网络适配器状态](./hyper-v-extensible-switch-port-and-network-adapter-states.md)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘完成 OID 交换机端口删除的 OID 设置 \_ 请求 \_ \_ ，并返回以下状态代码。

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
[*DereferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)

[**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[OID \_ 交换机 \_ NIC \_ 删除](oid-switch-nic-delete.md)

[OID \_ 交换机 \_ 端口 \_ 数组](oid-switch-port-array.md)

[*ReferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)

 

