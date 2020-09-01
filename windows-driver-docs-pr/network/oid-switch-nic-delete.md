---
title: OID_SWITCH_NIC_DELETE
description: Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 将 OID_SWITCH_NIC_DELETE 的请求设置为可扩展交换机驱动程序堆栈。
ms.assetid: 7564EA39-09F5-45A3-81A0-F8DD2B23B639
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_DELETE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3872a89a5b16fcc8f5f730434f5e45daf11c7f01
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206331"
---
# <a name="oid_switch_nic_delete"></a>OID \_ 交换机 \_ NIC \_ 删除


Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 将 OID \_ 交换机 NIC DELETE 的请求设置 \_ \_ 为可扩展交换机驱动程序堆栈。 此 OID 请求通知底层的可扩展交换机扩展，以了解如何删除可扩展交换机端口和网络适配器之间的连接。 可扩展交换机的协议边缘以前通知扩展，此连接在其发出 oid [ \_ 交换机 \_ NIC \_ 断开连接](oid-switch-nic-disconnect.md)的 oid 集请求时被删除。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构的指针。

<a name="remarks"></a>备注
-------

[**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构的**PortId**成员指定正在为其发出删除通知的端口。 可扩展交换机扩展可以通过发出 oid [ \_ 交换机 \_ 端口 \_ 数组](oid-switch-port-array.md)的 oid 查询请求，获取可扩展交换机上此端口和其他端口的参数信息。

[**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构的**index**成员指定正在为其发出删除通知的网络适配器的索引。 具有指定 **索引** 值的网络适配器连接到由 **PortId** 成员指定的可扩展交换机端口。 有关这些索引值的详细信息，请参阅 [网络适配器索引值](./network-adapter-index-values.md)。

在可扩展交换机的协议边缘发出 OID \_ 交换机 \_ NIC \_ DELETE 请求之前，它保证指定的网络适配器连接的所有挂起的发送或接收数据包请求均已完成。 协议边缘还保证适配器连接的所有挂起 OID 请求已完成，并且适配器连接的可扩展交换机引用计数器的值为零。

**注意**   如果扩展插件已通过调用[*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)增加网络适配器的可扩展交换机引用计数器，则在 \_ \_ \_ 引用计数器为非零值时，不会发出 OID 交换机 NIC DELETE 请求。 该扩展通过调用 [*DereferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)来递减可扩展的 switch 引用计数器。

 

扩展必须遵循以下准则来处理 OID \_ 交换机 NIC DELETE 的 oid 集 \_ 请求 \_ ：

-   扩展不得修改与 OID 请求关联的 [**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters) 结构。

-   扩展必须始终将此 OID 集请求转发到基础扩展。 扩展不能完成请求。

-   扩展不能发出自己的 OID set NIC DELETE 的请求 \_ \_ \_ 。

-   可扩展交换机外部网络适配器可以绑定到一个或多个基础物理适配器。 对于绑定到外部网络适配器的每个物理网络适配器，可扩展交换机的协议边缘会发出单独的 OID \_ 交换机 \_ NIC \_ 删除请求。 每个 OID 集请求指定一个不同的网络适配器连接索引值。 有关这些索引值的详细信息，请参阅 [网络适配器索引值](./network-adapter-index-values.md)。

    扩展必须维护每个基础物理适配器的连接状态。 有关可以将物理网络适配器绑定到外部网络适配器的不同配置的详细信息，请参阅 [物理网络适配器配置的类型](./types-of-physical-network-adapter-configurations.md)。

有关可扩展交换机端口和网络适配器连接状态的详细信息，请参阅 [Hyper-v 可扩展交换机端口和网络适配器状态](./hyper-v-extensible-switch-port-and-network-adapter-states.md)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘完成 OID 交换机 NIC DELETE 的 OID 查询 \_ 请求 \_ \_ ，并返回以下状态代码。

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
[*DereferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)

[OID \_ 交换机 \_ NIC \_ 断开连接](oid-switch-nic-disconnect.md)

[OID \_ 交换机 \_ 端口 \_ 数组](oid-switch-port-array.md)

[*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)

 

