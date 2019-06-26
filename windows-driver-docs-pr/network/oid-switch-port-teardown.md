---
title: OID_SWITCH_PORT_TEARDOWN
description: HYPER-V 可扩展交换机的协议边缘发出一个对象标识符 (OID) 组请求的 OID_SWITCH_PORT_TEARDOWN 通知基础可扩展交换机扩展的可扩展交换机端口将开始删除过程。
ms.assetid: 94FA23AC-2064-40C8-B99C-D8D3DC10BFF9
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_TEARDOWN 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5251c0d3f19f87352426c11c6050d852c5b5c93f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386984"
---
# <a name="oidswitchportteardown"></a>OID\_交换机\_端口\_拆解


HYPER-V 可扩展交换机的协议边缘发出对象标识符 (OID) 组请求的 OID\_切换\_端口\_拆卸通知基础可扩展交换机端口将可扩展交换机扩展开始删除过程。 协议驱动程序问题的 OID 集请求时启动此进程[OID\_交换机\_端口\_删除](oid-switch-port-delete.md)。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构。

<a name="remarks"></a>备注
-------

**PortId**的成员[ **NDIS\_切换\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构指定的可扩展交换机端口为其 connect 通知进行了。 可扩展的交换机扩展必须更新它按以下方式获取的端口有关的任何缓存的信息：

-   通过发出 OID 查询的请求[OID\_交换机\_端口\_数组](oid-switch-port-array.md)。 该扩展在发出此 OID [ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)时，才[OID\_开关\_参数](oid-switch-parameters.md)返回[ **NDIS\_交换机\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_parameters)结构**IsActive**设置为 TRUE。 如果**IsActive**为 FALSE 时，扩展问题 OID 时**NetEventSwitchActivate** [ **NET\_PNP\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event)扩展微型端口由颁发。

-   通过检查各种 OID 设置的请求[OID\_交换机\_端口\_创建](oid-switch-port-create.md)并[OID\_交换机\_端口\_删除](oid-switch-port-delete.md).

可扩展交换机的协议边缘发出 OID 集请求的 OID\_切换\_端口\_拆卸通知端口是正在从可扩展的交换机中删除的过程中的扩展。 颁发此 OID 请求之前，可扩展交换机的协议边缘之前必须颁发以下 Oid，如果端口有活动的网络适配器连接：

-   [OID\_交换机\_NIC\_断开连接](oid-switch-nic-disconnect.md)，该通知基础的网络适配器不再是扩展插件中指定的端口连接[ **NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构。

-   [OID\_切换\_NIC\_删除](oid-switch-nic-delete.md)，该通知基础扩展之间的网络适配器和可扩展交换机端口的网络连接已被删除。

    指定可扩展交换机端口的所有挂起的数据包被取消或完成后，协议边缘将发出此 OID 集请求。

可扩展交换机的协议边缘扩展完成此 OID 集请求并可扩展交换机端口的引用计数器为零后，颁发的 OID 集请求[OID\_切换\_端口\_删除](oid-switch-port-delete.md)。 此 OID 请求从可扩展的交换机中删除该端口。

**请注意**  扩展的可扩展交换机端口的引用计数器递增通过调用[ *ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)。 扩展递减引用计数器通过调用[ *DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_dereference_switch_port)。

 

扩展必须遵守以下原则处理 OID 设置请求的 OID\_交换机\_端口\_拆卸：

-   扩展始终将转发对基础扩展的 OID 集请求。 扩展必须不会使请求失败。

    **请注意**  扩展必须修改[ **NDIS\_开关\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)与关联的结构OID 请求。

     

-   该扩展将转发此 OID 请求后，它不能将数据包转发到已删除的端口。 扩展还不能发出 OID 请求，也不调用[ *ReferenceSwitchPort* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)函数已删除的端口。

**请注意**  扩展必须发出 OID 集请求的 OID\_交换机\_端口\_拆解。

 

有关可扩展交换机端口和网络适配器连接的状态的详细信息，请参阅[HYPER-V 可扩展交换机端口和网络适配器状态](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础的微型端口边缘完成 OID 集请求的 OID\_切换\_端口\_拆解，并返回以下状态代码。

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
<td><p>Version</p></td>
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[*DereferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_dereference_switch_port)

[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)

[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SWITCH\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_parameters)

[**NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)

[**NET\_PNP\_EVENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event)

[OID\_交换机\_NIC\_删除](oid-switch-nic-delete.md)

[OID\_SWITCH\_PARAMETERS](oid-switch-parameters.md)

[OID\_交换机\_端口\_数组](oid-switch-port-array.md)

[*ReferenceSwitchPort*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_port)

 

 




