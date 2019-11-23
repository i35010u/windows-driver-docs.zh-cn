---
title: OID_SWITCH_PORT_DELETE
description: Hyper-v 可扩展交换机的协议边缘发出 OID_SWITCH_PORT_DELETE 的对象标识符（OID）设置请求，通知有关如何删除可扩展交换机端口的可扩展交换机扩展。
ms.assetid: D8893395-3D33-4777-B8F0-4DD6BE9B8A37
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_DELETE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cc6a6dc81687bc9eb29d8b2b27c26e751c312c67
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843936"
---
# <a name="oid_switch_port_delete"></a>OID\_交换机\_端口\_删除


Hyper-v 可扩展交换机的协议边缘发出一个对象标识符（OID）设置的 OID 请求，\_交换机\_端口\_"删除"，以通知有关删除可扩展交换机端口的可扩展交换机扩展。

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_SWITCH\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构的指针。

<a name="remarks"></a>备注
-------

[**NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构的**PortId**成员指定了删除通知所针对的可扩展交换机端口。

如果网络适配器连接到指定的端口，则可扩展交换机的协议边缘将在删除该端口之前删除该连接。 在这种情况下，协议边缘将在删除端口之前执行以下步骤：

-   协议边缘发出 oid [\_SWITCH\_NIC](oid-switch-nic-disconnect.md)的 oid 集请求\_"断开连接"，通知扩展网络适配器与可扩展交换机端口之间的连接将被删除。

-   在已取消或完成指定的可扩展交换机端口的所有挂起数据包后，协议边缘会发出 oid [\_switch\_NIC](oid-switch-nic-delete.md)的 oid 集请求\_"删除"，通知扩展网络适配器与可扩展交换机端口之间的连接已被删除。

    此时，协议边缘可以开始删除该端口。

可扩展交换机的协议边缘在删除可扩展交换机端口时遵循以下步骤：

1.  可扩展交换机的协议边缘[\_交换机\_端口\_拆卸](oid-switch-port-teardown.md)发出 OID 的 oid 集请求。 此 OID 请求通知底层的可扩展交换机扩展，了解有关可扩展交换机端口的删除过程的开始。

2.  协议边缘发出 oid\_SWITCH\_端口的 OID 集请求，在对可扩展交换机端口的所有 OID 请求都完成之后，\_删除。

    **请注意**  扩展之前是否调用了[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)来递增端口的引用计数器，则必须先调用[*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port) ，然后协议边缘[\_交换机\_NIC\_删除](oid-switch-nic-delete.md)请求。

     

此扩展必须遵循以下准则，以便处理 OID\_SWITCH\_端口\_删除的 OID 集请求：

-   扩展不能修改与 OID 请求关联的[**NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构。

-   扩展必须始终将此 OID 集请求转发到基础扩展。 此扩展不能导致请求失败。

-   在 OID\_交换机\_端口完成，\_删除请求完成，NDIS\_状态\_成功，该扩展将不会接收到已删除端口的任何数据包或 OID 请求。 此扩展无法将数据包转发到已删除的端口。 扩展还不能为已删除的端口发出 OID 请求，也不能调用[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)函数。

**请注意**  可扩展交换机扩展不得\_交换机\_端口\_删除发出 oid set 请求。

 

有关可扩展交换机端口和网络适配器连接状态的详细信息，请参阅[Hyper-v 可扩展交换机端口和网络适配器状态](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘完成 OID\_SWITCH\_端口的 OID 集请求\_删除并返回以下状态代码。

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
[*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[OID\_交换机\_NIC\_删除](oid-switch-nic-delete.md)

[OID\_交换机\_端口\_数组](oid-switch-port-array.md)

[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)

 

 




