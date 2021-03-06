---
title: OID_SWITCH_NIC_DISCONNECT
description: Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID_SWITCH_NIC_DISCONNECT 请求，通知底层可扩展交换机端口与网络适配器之间的连接已被破坏。 完全断开连接后，可扩展交换机的协议边缘将发出 OID_SWITCH_NIC_DELETE 的 OID 设置请求。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_DISCONNECT 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f6d5b2d6d35d1d9c4ad99f4bbdc816bbae919dc0
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102247919"
---
# <a name="oid_switch_nic_disconnect"></a>OID \_ 交换机 \_ NIC \_ 断开连接


Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID 交换机 NIC 断开连接的请求， \_ \_ \_ 通知底层可扩展交换机端口与网络适配器之间的连接被切断。 完全断开连接后，可扩展交换机的协议边缘将发出 oid [ \_ 交换机 \_ NIC \_ DELETE](oid-switch-nic-delete.md)的 oid 设置请求。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构的指针。

<a name="remarks"></a>备注
-------

[**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构的 **index** 成员指定为其发出断开连接通知的网络适配器的索引。 具有指定 **索引** 值的网络适配器连接到由 **PortId** 成员指定的可扩展交换机端口。 有关这些索引值的详细信息，请参阅 [网络适配器索引值](./network-adapter-index-values.md)。

当扩展处理 OID \_ 交换机 \_ NIC 断开连接的 oid 集请求时，必须遵循以下准则 \_ ：

-   扩展不得修改与 OID 请求关联的 [**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters) 结构。

-   OID \_ 交换机 \_ NIC \_ 断开连接请求仅通知扩展：在指定的网络适配器和可扩展交换机端口之间断开可扩展交换机连接。 扩展处理此 OID 请求后，不能执行以下操作：

    -   为 \_ 发出 oid 交换机 \_ NIC 断开 oid 请求的可扩展交换机端口上的网络适配器连接生成任何数据包流量 \_ 。

    -   调用 [*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) ，以在可扩展交换机端口上为指定网络适配器连接递增可扩展交换机引用计数器。

    -   将 Oid 交换机 nic 请求的 oid 请求转发或发起 oid [ \_ 交换机 \_ nic \_ 请求](oid-switch-nic-request.md) 发送到的基础网络适配器 \_ \_ \_ 。

        **注意**  如果在发出 OID 交换机 NIC 断开连接之前调用 [*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) 的扩展来递增可扩展交换机引用计数器 \_ \_ \_ ，则扩展仍可转发或发起 oid 请求。



    -   从为其发出 OID 交换机 nic 断开 OID 请求的基础网络适配器转发或产生 ndis 状态 [**\_ \_ 切换 \_ nic \_ 状态**](./ndis-status-switch-nic-status.md) 的 ndis 状态指示 \_ \_ \_ 。

        **注意**  如果在发出 OID 交换机 NIC 断开连接之前调用 [*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) 的扩展来递增可扩展交换机引用计数器 \_ \_ \_ ，则扩展仍可转发或产生 NDIS 状态指示。

        **注意**  如果扩展之前调用 [*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic) 来递增可扩展交换机引用计数器，则不需要将其调用与管理 hyper-v 可扩展交换机 OID 请求的代码进行同步或转发 OID 请求或 NDIS 状态指示。 扩展增量引用计数器之后，可扩展交换机接口不会发出 oid [ \_ 交换机 \_ NIC \_ DELETE](oid-switch-nic-delete.md)的 oid 设置请求。

-   扩展必须始终将此 OID 集请求转发到基础扩展。 扩展不能完成请求。

-   可扩展交换机外部网络适配器可以绑定到一个或多个基础物理适配器。 对于绑定到外部网络适配器的每个物理网络适配器，可扩展交换机的协议边缘会发出单独的 OID \_ 交换机 \_ NIC \_ 断开连接请求。 每个 OID 集请求指定一个不同的网络适配器连接索引值。 有关这些索引值的详细信息，请参阅 [网络适配器索引值](./network-adapter-index-values.md)。

    扩展必须维护每个基础物理适配器的连接状态。 有关可以将物理网络适配器绑定到外部网络适配器的不同配置的详细信息，请参阅 [物理网络适配器配置的类型](./types-of-physical-network-adapter-configurations.md)。

**注意**  扩展不能发出自己的 OID set \_ \_ NIC 交换机 NIC \_ 断开连接请求。

有关可扩展交换机端口和网络适配器连接状态的详细信息，请参阅 [Hyper-v 可扩展交换机端口和网络适配器状态](./hyper-v-extensible-switch-port-and-network-adapter-states.md)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘完成 OID \_ 交换机 NIC 断开连接的 oid 查询 \_ 请求 \_ ，并返回以下状态代码。

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
[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS \_ 交换机 \_ NIC \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)

[OID \_ 交换机 \_ NIC \_ 删除](oid-switch-nic-delete.md)

[OID \_ 交换机 \_ 端口 \_ 数组](oid-switch-port-array.md)

[*ReferenceSwitchPort*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)
