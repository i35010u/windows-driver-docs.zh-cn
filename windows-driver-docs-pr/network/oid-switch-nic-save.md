---
title: OID_SWITCH_NIC_SAVE
description: Hyper-v 可扩展交换机的协议边缘发出对象标识符 (OID 在操作过程中 OID_SWITCH_NIC_SAVE) 方法请求，以保存可扩展交换机端口及其网络适配器连接的运行时数据。
ms.assetid: FE2F9767-7186-42FF-85C1-2A8203FEF629
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_SAVE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f278e5855eb77d3827effb778d81d1934127fb7e
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107208"
---
# <a name="oid_switch_nic_save"></a>OID \_ 交换机 \_ NIC \_ 保存


Hyper-v 可扩展交换机的协议边缘发出对象标识符 () OID \_ \_ \_ 在操作期间进行 oid 交换机 NIC 保存，以保存可扩展交换机端口及其网络适配器连接的运行时数据。 该扩展将返回此数据，以便以后可以保存和还原运行时数据。 保存运行时数据后，它将通过 oid [ \_ 交换机 \_ NIC \_ 还原](oid-switch-nic-restore.md)的 oid 设置请求进行还原。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构的指针。 此结构由可扩展交换机的协议边缘分配。

<a name="remarks"></a>注解
-------

当收到 oid 交换机 NIC SAVE 的 OID 方法请求时 \_ \_ \_ ，可扩展交换机扩展通过执行以下操作来保存运行时数据：

-   该扩展将数据保存在 [**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state) 结构内，从结构的开头开始 *SaveDataOffset* 字节。

-   如果提供的 *SaveDataSize* 不够大，无法容纳所需的保存数据，则该扩展会将方法结构的 *BytesNeeded* 字段设置为 ndis \_ SIZEOF \_ ndis \_ SWITCH \_ NIC \_ 保存 \_ 状态 \_ 修订 \_ 1，以及保存保存数据所需的缓冲区数量，并通过 NDIS \_ 状态缓冲区完成 OID \_ \_ 太 \_ 短。 将重新颁发具有所需大小的 OID。

-   该扩展将用自己的标识符和名称填充 *ExtensionId* 和 *ExtensionFriendlyName* 字段，并完成具有 NDIS 状态成功的 OID 方法请求 \_ \_ 。 这会导致可扩展交换机的协议边缘发出另一个 OID 方法请求，以允许扩展返回更多的保存数据，或允许其他扩展关闭堆栈以保存其自己的数据。

**注意**   如果该扩展没有要保存的运行时数据，则必须调用[**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)将此 OID 方法请求转发到可扩展交换机驱动程序堆栈中的基础扩展。 有关此过程的详细信息，请参阅 [在 NDIS 筛选器驱动程序中筛选 OID 请求](./filtering-oid-requests-in-an-ndis-filter-driver.md)。

 

Hyper-v 可扩展交换机在发出 OID 之前填充结构的 *标头*、 *PortId*、 *NicIdex*、 *SaveDataSize* 和 *SaveDataOffset* 字段。 扩展无法修改这些字段。

OID 交换机 NIC SAVE 的 OID 方法请求 \_ \_ \_ 最终由可扩展交换机的基础微型端口边缘处理。 在可扩展交换机的微型端口边缘收到此 OID 方法请求后，它将完成具有 NDIS 状态成功的 OID 请求 \_ \_ 。 这会通知可扩展交换机的协议边缘已查询了运行时数据的可扩展交换机驱动程序堆栈中的所有扩展。 然后，可扩展交换机的协议边缘发出 oid [ \_ 交换机 \_ NIC \_ save \_ 完成](oid-switch-nic-save-complete.md) 的 oid 集请求，以完成保存操作。

有关如何为可扩展交换机端口保存运行时数据的详细信息，请参阅 [保存 Hyper-v 可扩展交换机运行时数据](./managing-hyper-v-extensible-switch-run-time-data.md)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机扩展为 OID \_ 交换机 NIC SAVE 的 oid 方法请求返回以下状态代码之一 \_ \_ 。

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
<td><p>NDIS_STATUS_BUFFER_TOO_SHORT</p></td>
<td><p>信息缓冲区的长度太小，无法用于 <a href="/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_NIC_SAVE_STATE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)"><strong>NDIS_SWITCH_NIC_SAVE_STATE</strong></a> 及其相关联的运行时数据。可扩展交换机扩展必须设置 <strong>数据。METHOD_INFORMATION。</strong> 将 <a href="/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a> 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>如果扩展正在返回要保存的运行时数据，则会返回此状态。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>由于其他原因，请求失败。</p></td>
</tr>
</tbody>
</table>

 

可扩展交换机的基础微型端口边缘为 OID \_ 交换机 NIC SAVE 的 oid 方法请求返回以下状态代码 \_ \_ 。

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

## <a name="see-also"></a>请参阅


****
[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ 交换机 \_ NIC \_ 保存 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)

[**NdisFOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[OID \_ 交换机 \_ NIC \_ 还原](oid-switch-nic-restore.md)

[OID \_ 交换机 \_ NIC \_ 保存 \_ 完毕](oid-switch-nic-save-complete.md)

