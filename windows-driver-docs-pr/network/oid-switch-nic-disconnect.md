---
title: OID_SWITCH_NIC_DISCONNECT
description: Hyper-v 可扩展交换机的协议边缘发出 OID_SWITCH_NIC_DISCONNECT 的对象标识符（OID）设置请求，通知底层可扩展交换机端口与网络适配器之间的连接正在断。 完全断开连接后，可扩展交换机的协议边缘将发出 OID_SWITCH_NIC_DELETE 的 OID 设置请求。
ms.assetid: 367081A7-F259-4132-B857-C956C0F2829C
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_DISCONNECT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d665c102aa66c98d2b02836d458d48baf5dcfe4c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843956"
---
# <a name="oid_switch_nic_disconnect"></a>OID\_交换机\_NIC\_断开连接


Hyper-v 可扩展交换机的协议边缘发出 OID\_交换机的对象标识符（OID）设置请求\_NIC\_"断开连接"，通知底层可扩展交换机端口与网络适配器已被破坏。 完全断开连接后，可扩展交换机的协议边缘将[\_交换机\_NIC\_删除](oid-switch-nic-delete.md)发出 OID 的 oid 设置请求。

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_SWITCH\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构的指针。

<a name="remarks"></a>备注
-------

NDIS\_交换机的**索引**成员[ **\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构指定正在为其发出断开连接通知的网络适配器的索引。 具有指定**索引**值的网络适配器连接到由**PortId**成员指定的可扩展交换机端口。 有关这些索引值的详细信息，请参阅[网络适配器索引值](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)。

此扩展在处理 OID 的 OID 集请求时必须遵循这些准则\_交换机\_NIC\_断开连接：

-   扩展不能修改与 OID 请求关联[ **\_NIC\_参数结构的 NDIS\_开关**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)。

-   OID\_交换机\_NIC\_DISCONNECT 请求仅通知扩展：在指定的网络适配器和可扩展交换机端口之间，可扩展交换机连接将被断开。 扩展处理此 OID 请求后，不能执行以下操作：

    -   在可扩展交换机端口上生成与 OID\_交换机\_NIC\_断开 OID 请求的网络适配器连接的任何数据包流量。

    -   调用[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) ，以在可扩展交换机端口上为指定网络适配器连接递增可扩展交换机引用计数器。

    -   转发或发起 oid [\_交换机\_nic\_请求请求发送到请求](oid-switch-nic-request.md)的基础网络适配器，该适配器会向其发出 OID\_开关\_NIC\_断开 oid 请求。

        **注意** 如果名为[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)的扩展在\_交换机\_\_NIC 之前递增可扩展交换机引用计数器，则该扩展仍可转发或发起 OID 请求。



    -   转发或产生 Ndis\_状态的 NDIS 状态指示[ **\_交换机\_nic\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-switch-nic-status)的基础网络适配器，该适配器为其发出 OID\_交换机\_NIC\_断开连接 OID 请求。

        **注意** 如果名为[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)的扩展在\_交换机\_\_NIC 之前递增可扩展交换机引用计数器，则该扩展仍可转发或产生 NDIS 状态指示。

        **注意** 如果扩展之前调用了[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)来递增可扩展交换机引用计数器，则不需要将其调用与管理 hyper-v 的代码同步或转发 OID 请求或 NDIS 状态指示可扩展的 switch OID 请求。 扩展增量引用计数器之后，可扩展交换机接口将不会[\_NIC\_交换机 NIC\_删除](oid-switch-nic-delete.md)发出 oid 设置请求。

-   扩展必须始终将此 OID 集请求转发到基础扩展。 扩展不能完成请求。

-   可扩展交换机外部网络适配器可以绑定到一个或多个基础物理适配器。 对于绑定到外部网络适配器的每个物理网络适配器，可扩展交换机的协议边缘\_NIC\_断开连接时发出\_交换机的单独 OID 集请求。 每个 OID 集请求指定一个不同的网络适配器连接索引值。 有关这些索引值的详细信息，请参阅[网络适配器索引值](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)。

    扩展必须维护每个基础物理适配器的连接状态。 有关可以将物理网络适配器绑定到外部网络适配器的不同配置的详细信息，请参阅[物理网络适配器配置的类型](https://docs.microsoft.com/windows-hardware/drivers/network/types-of-physical-network-adapter-configurations)。

**注意** 扩展不能\_NIC\_交换机上发出其自己的 OID 设置请求，\_断开连接。

有关可扩展交换机端口和网络适配器连接状态的详细信息，请参阅[Hyper-v 可扩展交换机端口和网络适配器状态](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘\_交换机\_NIC 上完成 oid 查询请求，\_断开连接并返回以下状态代码。

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

[OID\_交换机\_NIC\_删除](oid-switch-nic-delete.md)

[OID\_交换机\_端口\_数组](oid-switch-port-array.md)

[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)