---
title: OID_SWITCH_PORT_UPDATED
description: Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID_SWITCH_PORT_UPDATED 请求，以通知有关可扩展交换机端口更新的可扩展交换机扩展。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_UPDATED 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c22449e30a52a9454a6c4c81f6683a3f2269bf8c
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249173"
---
# <a name="oid_switch_port_updated"></a>\_ \_ 已更新 OID 交换机端口 \_


Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 \_ 已更新 oid 交换机端口的请求 \_ \_ ，以通知可扩展交换机扩展有关更新可扩展交换机端口的信息。 仅对已创建且尚未开始拆卸/删除进程的端口发出 OID。 目前，只有 **PortFriendlyName** 字段在创建后可能会更新。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**ndis \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构的指针。

<a name="remarks"></a>备注
-------

[**NDIS \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)结构的 **PortId** 成员指定进行更新通知的可扩展交换机端口。

扩展必须遵循以下准则，以便处理 \_ 已更新 oid 交换机端口的 oid 集请求 \_ \_ ：

-   扩展不得修改与 OID 请求关联的 [**NDIS \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters) 结构。

-   扩展必须始终将此 OID 集请求转发到基础扩展。 此扩展不能导致请求失败。

**注意**  可扩展交换机扩展不得颁发 oid \_ 交换机端口更新的 oid 设置 \_ 请求 \_ 。

 

有关可扩展交换机端口和网络适配器连接状态的详细信息，请参阅 [Hyper-v 可扩展交换机端口和网络适配器状态](./hyper-v-extensible-switch-port-and-network-adapter-states.md)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础微型端口边缘完成 oid 交换机端口的 OID 设置请求 \_ \_ \_ ，并返回以下状态代码。

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
[*DereferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_dereference_switch_nic)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS \_ 交换机 \_ 端口 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_parameters)

[**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[OID \_ 交换机 \_ NIC \_ 删除](oid-switch-nic-delete.md)

[OID \_ 交换机 \_ 端口 \_ 数组](oid-switch-port-array.md)

[*ReferenceSwitchNic*](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_reference_switch_nic)

 

