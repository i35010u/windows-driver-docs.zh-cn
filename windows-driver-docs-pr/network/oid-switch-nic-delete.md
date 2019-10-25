---
title: OID_SWITCH_NIC_DELETE
description: Hyper-v 可扩展交换机的协议边缘向可扩展交换机驱动程序堆栈发出 OID_SWITCH_NIC_DELETE 的对象标识符（OID）设置请求。
ms.assetid: 7564EA39-09F5-45A3-81A0-F8DD2B23B639
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_DELETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b192b27fecb423aa450be4de6323f082fc517f6b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843957"
---
# <a name="oid_switch_nic_delete"></a>OID\_交换机\_NIC\_删除


Hyper-v 可扩展交换机的协议边缘发出\_交换机\_NIC 的对象标识符（OID）设置请求，\_删除到可扩展交换机驱动程序堆栈。 此 OID 请求通知底层的可扩展交换机扩展，以了解如何删除可扩展交换机端口和网络适配器之间的连接。 可扩展交换机的协议边缘先前通知了此连接在发出 oid [\_switch\_NIC\_断开](oid-switch-nic-disconnect.md)连接时将被删除的扩展。

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_SWITCH\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构的指针。

<a name="remarks"></a>备注
-------

NDIS\_交换机的**PortId**成员[ **\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构指定正在为其发出删除通知的端口。 可扩展交换机扩展可以通过发出 oid [\_switch\_端口\_数组](oid-switch-port-array.md)的 oid 查询请求，获取可扩展交换机上此端口和其他端口的参数信息。

NDIS\_交换机的**索引**成员[ **\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构指定正在为其发出删除通知的网络适配器的索引。 具有指定**索引**值的网络适配器连接到由**PortId**成员指定的可扩展交换机端口。 有关这些索引值的详细信息，请参阅[网络适配器索引值](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)。

在可扩展交换机的协议边缘发出 OID\_交换机\_NIC\_DELETE 请求，保证指定的网络适配器连接的所有挂起的发送或接收数据包请求均已完成。 协议边缘还保证适配器连接的所有挂起 OID 请求已完成，并且适配器连接的可扩展交换机引用计数器的值为零。

**请注意**  如果扩展插件已通过调用[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)增加网络适配器的可扩展交换机引用计数器，则不会\_\_\_在引用计数器为非零值。 该扩展通过调用[*DereferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)来递减可扩展的 switch 引用计数器。

 

扩展必须遵循以下准则，以便处理 OID\_SWITCH\_NIC\_删除的 OID 集请求：

-   扩展不能修改与 OID 请求关联[ **\_NIC\_参数结构的 NDIS\_开关**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)。

-   扩展必须始终将此 OID 集请求转发到基础扩展。 扩展不能完成请求。

-   扩展不能\_NIC\_交换机上颁发自己的 OID 设置请求，\_删除。

-   可扩展交换机外部网络适配器可以绑定到一个或多个基础物理适配器。 对于绑定到外部网络适配器的每个物理网络适配器，可扩展交换机的协议边缘向\_NIC\_删除 NIC 的单独 OID 集请求发出\_交换机。 每个 OID 集请求指定一个不同的网络适配器连接索引值。 有关这些索引值的详细信息，请参阅[网络适配器索引值](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)。

    扩展必须维护每个基础物理适配器的连接状态。 有关可以将物理网络适配器绑定到外部网络适配器的不同配置的详细信息，请参阅[物理网络适配器配置的类型](https://docs.microsoft.com/windows-hardware/drivers/network/types-of-physical-network-adapter-configurations)。

有关可扩展交换机端口和网络适配器连接状态的详细信息，请参阅[Hyper-v 可扩展交换机端口和网络适配器状态](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘\_交换机\_NIC 上完成 oid 查询请求\_删除并返回以下状态代码。

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
[*DereferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[ **\_NIC\_参数的 NDIS\_交换机**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)

[OID\_交换机\_NIC\_断开连接](oid-switch-nic-disconnect.md)

[OID\_交换机\_端口\_数组](oid-switch-port-array.md)

[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)

 

 




