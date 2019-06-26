---
title: OID_SWITCH_NIC_SAVE
description: 对象标识符 (OID) 方法的请求的 OID_SWITCH_NIC_SAVE 在操作过程中保存的可扩展交换机端口和其网络适配器连接运行时数据的 HYPER-V 可扩展交换机问题协议边缘。
ms.assetid: FE2F9767-7186-42FF-85C1-2A8203FEF629
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_SAVE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 23c2a7f8d71446b72d2b0dd8d7bc44aeed1b4ec6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385499"
---
# <a name="oidswitchnicsave"></a>OID\_交换机\_NIC\_保存


HYPER-V 可扩展交换机的协议边缘发出对象标识符 (OID) 方法请求的 OID\_切换\_NIC\_保存在保存可扩展交换机端口和其网络适配器的运行时数据的操作过程连接。 该扩展，以便运行时数据可以保存并还原在更高版本时返回此数据。 运行时数据将保存之后，它通过 OID 的集请求还原[OID\_交换机\_NIC\_还原](oid-switch-nic-restore.md)。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_交换机\_NIC\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构。 可扩展交换机的协议边缘分配了此结构。

<a name="remarks"></a>备注
-------

当它收到 OID 方法请求的 OID\_切换\_NIC\_保存，可扩展交换机扩展保存运行时数据执行以下操作：

-   该扩展将中的数据保存[ **NDIS\_交换机\_NIC\_保存\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)结构从开始*SaveDataOffset*从结构开始的字节数。

-   如果*SaveDataSize*提供不是足够大以保存所需保存数据，请扩展设置的方法结构*BytesNeeded*字段到 NDIS\_SIZEOF\_NDIS\_交换机\_NIC\_保存\_状态\_修订\_1 加上保存在保存所需的缓冲区的数据，并完成用 NDIS OID\_状态\_缓冲区\_过\_短。 使用所需的大小，将重新颁发 OID。

-   该扩展填充*ExtensionId*并*ExtensionFriendlyName*字段具有其自己的标识符和名称，并完成用 NDIS OID 方法请求\_状态\_成功。 这会导致发出另一个 OID 方法请求，以允许为扩展插件的可扩展交换机的协议边缘返回保存数据，或允许其他扩展的详细信息下堆栈上要保存其自己的数据。

**请注意**  如果扩展不具有运行时数据将保存，则必须调用[ **NdisFOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)此 OID 方法请求转发到中的基础扩展可扩展交换机驱动程序堆栈。 有关此过程的详细信息，请参阅[NDIS 筛选器驱动程序中筛选 OID 请求](https://docs.microsoft.com/windows-hardware/drivers/network/filtering-oid-requests-in-an-ndis-filter-driver)。

 

HYPER-V 可扩展交换机填充*标头*， *PortId*， *NicIdex*， *SaveDataSize*和*SaveDataOffset*之前发出 OID 结构的字段。 该扩展不能修改这些字段。

OID 方法请求的 OID\_切换\_NIC\_保存最终由可扩展交换机的基础的微型端口边缘。 可扩展交换机的微型端口边缘收到此 OID 方法请求后，它完成 OID 请求使用 NDIS\_状态\_成功。 这会通知可扩展交换机的协议边缘可扩展交换机驱动程序堆栈中的所有扩展已被都查询的运行时数据。 可扩展交换机的协议边缘然后颁发的 OID 集请求[OID\_切换\_NIC\_保存\_完成](oid-switch-nic-save-complete.md)完成保存操作。

有关如何将保存为可扩展交换机端口的运行时数据的详细信息，请参阅[保存的 HYPER-V 可扩展切换运行时数据](https://docs.microsoft.com/windows-hardware/drivers/network/saving-hyper-v-extensible-switch-run-time-data)。

### <a name="return-status-codes"></a>返回状态代码

可扩展的交换机扩展返回一个 OID 的 OID 方法请求的以下状态代码\_切换\_NIC\_保存。

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
<td><p>信息缓冲区长度太小<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state" data-raw-source="[&lt;strong&gt;NDIS_SWITCH_NIC_SAVE_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)"> <strong>NDIS_SWITCH_NIC_SAVE_STATE</strong> </a>可扩展交换机扩展必须设置及其相关运行时数据<strong>数据。METHOD_INFORMATION。BytesNeeded</strong>中的成员<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request" data-raw-source="[&lt;strong&gt;NDIS_OID_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)"> <strong>NDIS_OID_REQUEST</strong> </a>是必需的最小缓冲区大小的结构。</p></td>
</tr>
<tr class="even">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>如果它返回运行时数据将保存，扩展插件会返回此状态。</p></td>
</tr>
<tr class="odd">
<td><p>NDIS_STATUS_<em>Xxx</em></p></td>
<td><p>请求由于其他原因而失败。</p></td>
</tr>
</tbody>
</table>

 

可扩展交换机的基础的微型端口边缘返回 OID 的 OID 方法请求的以下状态代码\_切换\_NIC\_保存。

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
[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SWITCH\_NIC\_SAVE\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_save_state)

[**NdisFOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfoidrequest)

[OID\_SWITCH\_NIC\_RESTORE](oid-switch-nic-restore.md)

[OID\_交换机\_NIC\_保存\_完成](oid-switch-nic-save-complete.md)

 

 




