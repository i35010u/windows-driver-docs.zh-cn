---
title: OID_SWITCH_NIC_SAVE
description: Hyper-v 可扩展交换机的协议边缘在操作过程中发出 OID_SWITCH_NIC_SAVE 的对象标识符（OID）方法请求，以保存可扩展交换机端口及其网络适配器连接的运行时数据。
ms.assetid: FE2F9767-7186-42FF-85C1-2A8203FEF629
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_SAVE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 124188f6bf80e4de7c10462789d4db71b583bfef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843945"
---
# <a name="oid_switch_nic_save"></a>OID\_交换机\_NIC\_保存


Hyper-v 可扩展交换机的协议边缘发出\_交换机\_NIC 的对象标识符（OID）方法请求，\_在操作过程中保存以保存可扩展交换机端口及其网络适配器连接的运行时数据。 该扩展将返回此数据，以便以后可以保存和还原运行时数据。 保存运行时数据后，将通过 oid [\_交换机\_NIC\_还原](oid-switch-nic-restore.md)将其还原。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_SWITCH\_NIC 的指针\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构。 此结构由可扩展交换机的协议边缘分配。

<a name="remarks"></a>备注
-------

当接收到 oid 的 OID 方法请求时\_交换机\_NIC\_SAVE，可扩展交换机扩展通过执行以下操作来保存运行时数据：

-   该扩展将数据保存在[**NDIS\_交换机\_NIC\_SAVE\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构，从结构的开头开始*SaveDataOffset*字节。

-   如果提供的*SaveDataSize*不够大，无法容纳所需的保存数据，则扩展会将方法结构的*BytesNeeded*字段设置为 NDIS\_SIZEOF\_NDIS\_交换机\_NIC\_保存\_状态\_修订版本\_1 加上保存数据所需的缓冲区量，并通过 NDIS\_状态\_缓冲区来完成 OID，\_太短。 将重新颁发具有所需大小的 OID。

-   该扩展将用自己的标识符和名称填充*ExtensionId*和*ExtensionFriendlyName*字段，并通过 NDIS\_状态完成 OID 方法请求\_成功。 这会导致可扩展交换机的协议边缘发出另一个 OID 方法请求，以允许扩展返回更多的保存数据，或允许其他扩展关闭堆栈以保存其自己的数据。

**请注意**  如果扩展没有要保存的运行时数据，则必须调用[**NDISFOIDREQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)将此 OID 方法请求转发到可扩展交换机驱动程序堆栈中的基础扩展。 有关此过程的详细信息，请参阅[在 NDIS 筛选器驱动程序中筛选 OID 请求](https://docs.microsoft.com/windows-hardware/drivers/network/filtering-oid-requests-in-an-ndis-filter-driver)。

 

Hyper-v 可扩展交换机在发出 OID 之前填充结构的*标头*、 *PortId*、 *NicIdex*、 *SaveDataSize*和*SaveDataOffset*字段。 扩展无法修改这些字段。

OID\_SWITCH\_\_NIC 的 OID 方法请求最终由可扩展交换机的基础微型端口边缘处理。 在可扩展交换机的微型端口边缘收到此 OID 方法请求后，它将使用 NDIS\_状态完成 OID 请求，\_成功。 这会通知可扩展交换机的协议边缘已查询了运行时数据的可扩展交换机驱动程序堆栈中的所有扩展。 然后，可扩展交换机的协议边缘发出 oid\_交换机的 OID 集请求[\_NIC\_保存\_完成](oid-switch-nic-save-complete.md)来完成保存操作。

有关如何为可扩展交换机端口保存运行时数据的详细信息，请参阅[保存 Hyper-v 可扩展交换机运行时数据](https://docs.microsoft.com/windows-hardware/drivers/network/saving-hyper-v-extensible-switch-run-time-data)。

### <a name="return-status-codes"></a>返回状态代码

对于 OID\_SWITCH\_NIC\_"保存"，可扩展交换机扩展返回以下状态代码之一。

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
<td><p>NDIS_STATUS_BUFFER_TOO_SHORT</p></td>
<td><p>对于<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_NIC_SAVE_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)"><strong>NDIS_SWITCH_NIC_SAVE_STATE</strong></a>及其关联的运行时数据，信息缓冲区的长度太小。可扩展交换机扩展必须设置<strong>数据。METHOD_INFORMATION.</strong> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)"><strong>NDIS_OID_REQUEST</strong></a>结构中的 BytesNeeded 成员到所需的最小缓冲区大小。</p></td>
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

 

可扩展交换机的基础微型端口边缘为 OID\_SWITCH\_NIC\_保存的 OID 方法请求返回以下状态代码。

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

[**NDIS\_交换机\_NIC\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfoidrequest)

[OID\_交换机\_NIC\_还原](oid-switch-nic-restore.md)

[OID\_交换机\_NIC\_保存\_完成](oid-switch-nic-save-complete.md)

 

 




