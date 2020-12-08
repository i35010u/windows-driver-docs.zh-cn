---
title: OID_SWITCH_NIC_RESTORE
description: Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID_SWITCH_NIC_RESTORE 请求，以通知可扩展交换机扩展有关可为可扩展交换机端口及其网络适配器连接还原的运行时数据。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_RESTORE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d3d772f0a59261d18ac8719f028c4de8a279006b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836313"
---
# <a name="oid_switch_nic_restore"></a>OID \_ 交换机 \_ NIC \_ 还原


Hyper-v 可扩展交换机的协议边缘 (OID 发出对象标识符) 设置 OID \_ 交换机 \_ NIC 还原的请求 \_ ，以通知可扩展交换机扩展有关可为可扩展交换机端口及其网络适配器连接还原的运行时数据。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**ndis \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构的指针。 此结构由可扩展交换机的协议边缘分配。

<a name="remarks"></a>备注
-------

当其收到 oid 交换机 NIC 还原的 OID 集请求时 \_ \_ \_ ，可扩展交换机扩展必须首先确定它是否拥有运行时数据。 此扩展通过将 [**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构的 **ExtensionId** 成员的值与扩展用于标识自身的 GUID 值进行比较来实现此功能。

如果扩展插件拥有可扩展交换机端口的运行时数据，则将按以下方式还原这些数据：

1.  该扩展将 **SaveData** 成员中的运行时数据复制到扩展分配的存储中。

    **注意** [**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构的 **PortId** 成员的值可能与保存运行时数据时的 **PortId** 值不同。 如果在实时迁移从一台主机到另一台主机时保存了运行时数据，则会发生这种情况。 但是，可扩展交换机端口的配置会在实时迁移时保留。 这使该扩展可以使用新的 **PortId** 值将运行时数据还原到可扩展交换机端口。

     

2.  扩展完成 OID 集请求，NDIS 状态为 \_ " \_ 成功"。

如果扩展不拥有指定的运行时数据，则扩展将调用 [**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest) 将此 OID 集请求转发到可扩展交换机驱动程序堆栈中的基础扩展。 在这种情况下，扩展不能修改与 OID 请求关联的 [**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state) 结构。

如果 OID \_ 交换机 \_ NIC \_ 还原集请求由可扩展交换机的微型端口边缘接收，则它将完成具有 NDIS 状态成功的 oid \_ 请求 \_ 。 这会通知可扩展交换机的协议边缘，其中没有扩展拥有运行时数据。

有关如何还原运行时数据的详细信息，请参阅 [还原 Hyper-v 可扩展交换机 Run-Time 数据](./managing-hyper-v-extensible-switch-run-time-data.md)。

**注意**  如果扩展无法进行 OID 设置请求，则可扩展交换机会使整个还原操作失败。 因此，在可能的情况下，扩展应避免在 OID 请求时失败。 例如，如果扩展无法分配还原运行时数据所需的资源，则在不还原运行时数据的情况下它无法正常工作的情况下，OID 请求应该会失败。 但是，如果扩展可以从失败条件中恢复，则不应使 OID 设置请求失败。

 

### <a name="return-status-codes"></a>返回状态代码

如果扩展完成 oid 交换机 NIC 还原的 OID 设置 \_ 请求 \_ \_ ，它将返回以下状态代码之一。

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
<tr class="even">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>由于其他原因，请求失败。</p></td>
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

## <a name="see-also"></a>请参阅


****
[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)

[**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

 

