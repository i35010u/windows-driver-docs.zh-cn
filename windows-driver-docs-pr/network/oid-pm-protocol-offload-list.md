---
title: OID_PM_PROTOCOL_OFFLOAD_LIST
description: 作为查询，过量驱动程序可以使用 OID_PM_PROTOCOL_OFFLOAD_LIST OID 来枚举基础网络适配器上设置的协议卸载。
ms.assetid: 95ace77b-e583-4611-8460-af67b4d4805d
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PM_PROTOCOL_OFFLOAD_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2b56a7e7dab666171abca749c408a610033162fd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844051"
---
# <a name="oid_pm_protocol_offload_list"></a>OID\_PM\_协议\_卸载\_列表


作为查询，过量驱动程序可以使用 OID\_PM\_协议\_卸载\_列表 OID 来枚举基础网络适配器上设置的协议卸载。 成功从 OID 查询请求返回后， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**ndis\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)的列表的指针描述当前处于活动状态的协议卸载的结构。

<a name="remarks"></a>备注
-------

NDIS 处理微型端口驱动程序的查询。 NDIS 驱动程序可以使用 OID\_PM\_协议\_卸载\_列表 OID，以获取在基础网络适配器上设置的协议卸载的列表。

对于列表中的每个[**NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构，NDIS 将**NextProtocolOffloadOffset**成员设置为距 OID 信息缓冲区开头的偏移量（即，缓冲区的开头[ **\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构指向）的 ndis**成员到**列表中的下一 NDIS\_PM\_协议\_卸载结构的开头。 列表中最后一个结构的**NextProtocolOffloadOffset**成员中的偏移量为零。

如果未在网络适配器上设置任何协议卸载，NDIS 将设置**数据。查询\_信息。BytesWritten** ndis\_OID 的成员\_请求结构为零并返回 ndis\_状态\_成功。 数据内的数据 **。查询\_InformationBuffer**成员不由 NDIS 修改。

NDIS 为请求返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>成功的 NDIS\_状态\_  
请求已成功完成。 **InformationBuffer**包含指向协议卸载列表的指针（如果有）。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_挂起  
请求正在等待完成。 最终状态代码和结果将传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_状态\_缓存\_\_太短  
信息缓冲区太短。 NDIS 设置**数据。查询\_信息。** \_OID 中的 BytesNeeded 成员\_请求结构到所需的最小缓冲区大小。

<a href="" id="ndis-status-failure"></a>\_故障时的 NDIS\_状态  
由于上述原因之外的原因，导致请求失败。

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
<td><p>在 NDIS 6.20 和更高版本中受支持。 未请求微型端口驱动程序。 （请参见 "备注" 部分。）</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)

 

 




