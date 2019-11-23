---
title: OID_SWITCH_PORT_UPDATED
description: Hyper-v 可扩展交换机的协议边缘发出 OID_SWITCH_PORT_UPDATED 的对象标识符（OID）设置请求，通知可扩展交换机扩展有关更新可扩展交换机端口的信息。
ms.assetid: 7FDC963A-92E4-49B2-AB77-FA9C92EEBC25
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_UPDATED 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 85ca05120af6b5e93967db03b59fad6a1613684c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843922"
---
# <a name="oid_switch_port_updated"></a>OID\_交换机\_端口\_更新


Hyper-v 可扩展交换机的协议边缘发出\_交换机\_端口的对象标识符（OID）设置请求，\_进行了更新，以通知有关可扩展交换机端口更新的可扩展交换机扩展。 仅对已创建且尚未开始拆卸/删除进程的端口发出 OID。 目前，只有**PortFriendlyName**字段在创建后可能会更新。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_SWITCH\_NIC 的指针\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构。

<a name="remarks"></a>备注
-------

[**NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构中的**PortId**成员指定了更新通知所针对的可扩展交换机端口。

扩展必须遵循以下准则，以便处理\_交换机\_端口\_更新的 OID 设置请求：

-   扩展不能修改与 OID 请求关联的[**NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构。

-   扩展必须始终将此 OID 集请求转发到基础扩展。 此扩展不能导致请求失败。

**请注意**  可扩展交换机扩展不得\_交换机\_端口\_发出 oid set 请求。

 

有关可扩展交换机端口和网络适配器连接状态的详细信息，请参阅[Hyper-v 可扩展交换机端口和网络适配器状态](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-port-and-network-adapter-states)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘完成 OID 的 OID 集请求\_SWITCH\_端口\_更新并返回以下状态代码。

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

[**NDIS\_交换机\_端口\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[OID\_交换机\_NIC\_删除](oid-switch-nic-delete.md)

[OID\_交换机\_端口\_数组](oid-switch-port-array.md)

[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)

 

 




