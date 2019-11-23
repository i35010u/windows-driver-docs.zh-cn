---
title: OID_SWITCH_PORT_TEARDOWN
description: Hyper-v 可扩展交换机的协议边缘发出 OID_SWITCH_PORT_TEARDOWN 的对象标识符（OID）设置请求，通知底层的可扩展交换机扩展，可扩展交换机端口将开始删除过程。
ms.assetid: 94FA23AC-2064-40C8-B99C-D8D3DC10BFF9
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_TEARDOWN 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 34e0375582c8ca1193cc19515985d1b8d77da67f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843924"
---
# <a name="oid_switch_port_teardown"></a>OID\_交换机\_端口\_拆卸


Hyper-v 可扩展交换机的协议边缘发出 OID\_交换机的对象标识符（OID）设置请求\_端口\_拆卸通知底层可扩展交换机扩展，可扩展交换机端口会开始删除正在. 此过程在以下情况下启动：协议驱动程序发出 oid 的 OID 集请求[\_SWITCH\_端口\_删除](oid-switch-port-delete.md)。

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_SWITCH\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构的指针。

<a name="remarks"></a>备注
-------

[**NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构中的**PortId**成员指定了连接通知的可扩展交换机端口。 可扩展交换机扩展必须按以下方式更新有关其获取的端口的任何缓存信息：

-   通过发出[oid\_SWITCH\_端口\_数组](oid-switch-port-array.md)的 oid 查询请求。 此扩展仅在以下情况下在[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)上发出此 Oid： [oid\_switch\_参数](oid-switch-parameters.md)返回[ **\_\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_parameters)结构，并将**IsActive**设置为 TRUE。 如果**IsActive**为 FALSE，则扩展小型端口发出**NETEVENTSWITCHACTIVATE** [**NET\_PNP\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)时，扩展会发出 OID。

-   通过检查各种 OID， [\_switch\_端口\_CREATE](oid-switch-port-create.md)和[OID\_SWITCH\_\_删除](oid-switch-port-delete.md)。

可扩展交换机的协议边缘\_交换机\_端口\_拆卸发出 oid 集请求，以通知扩展某个端口正在从可扩展交换机中删除。 在发出此 OID 请求之前，如果该端口具有活动的网络适配器连接，则可扩展交换机的协议边缘以前颁发了以下 Oid：

-   [OID\_交换机\_NIC\_"断开连接](oid-switch-nic-disconnect.md)"，这会通知基础扩展，指出网络适配器不再连接到[**NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)中指定的端口构造.

-   [OID\_交换机\_NIC\_DELETE](oid-switch-nic-delete.md)，这会通知基础扩展网络适配器与可扩展交换机端口之间的网络连接已删除。

    协议边缘在已取消或完成指定的可扩展交换机端口的所有挂起数据包后发出此 OID 集请求。

扩展完成此 OID 集请求并且可扩展交换机端口的引用计数器为零后，可扩展交换机的协议边缘会发出 oid [\_switch\_端口\_DELETE](oid-switch-port-delete.md)的 oid 设置请求。 此 OID 请求从可扩展交换机中删除端口。

**请注意**  扩展会通过调用[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)来递增可扩展交换机端口的引用计数器。 扩展通过调用[*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_port)来递减引用计数器。

 

扩展必须遵循以下准则，以便处理 OID\_SWITCH\_端口\_拆卸的 OID 集请求：

-   扩展必须始终将此 OID 集请求转发到基础扩展。 此扩展不能导致请求失败。

    **请注意**  扩展不得修改与 OID 请求关联[ **\_端口\_参数结构的 NDIS\_开关**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)。

     

-   扩展转发此 OID 请求后，它无法将数据包转发到删除的端口。 扩展还不能为已删除的端口发出 OID 请求，也不能调用[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)函数。

**请注意**  扩展不能\_交换机\_端口\_拆卸发出 oid set 请求。

 

有关可扩展交换机端口和网络适配器连接状态的详细信息，请参阅[Hyper-v 可扩展交换机端口和网络适配器状态](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘\_交换机\_端口\_拆卸完成 oid 设置请求，并返回以下状态代码。

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

[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SWITCH\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_parameters)

[**NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[**NET\_PNP\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)

[OID\_交换机\_NIC\_删除](oid-switch-nic-delete.md)

[OID\_SWITCH\_参数](oid-switch-parameters.md)

[OID\_交换机\_端口\_数组](oid-switch-port-array.md)

[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_port)

 

 




