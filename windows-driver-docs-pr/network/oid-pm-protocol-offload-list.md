---
title: OID_PM_PROTOCOL_OFFLOAD_LIST
description: 为查询，过量驱动程序可用于 OID_PM_PROTOCOL_OFFLOAD_LIST OID 枚举基础的网络适配器设置协议卸载。
ms.assetid: 95ace77b-e583-4611-8460-af67b4d4805d
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PM_PROTOCOL_OFFLOAD_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5f563ebb18f062c69796277d468aa611a4cc33cd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377063"
---
# <a name="oidpmprotocoloffloadlist"></a>OID\_PM\_协议\_卸载\_列表


为查询，过量驱动程序可以使用 OID\_PM\_协议\_卸载\_列表 OID 枚举基础的网络适配器设置协议卸载。 从 OID 查询请求，成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一系列的指针[ **NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)描述当前处于活动状态的协议的结构将卸载。

<a name="remarks"></a>备注
-------

NDIS 处理查询的微型端口驱动程序。 NDIS 驱动程序可以使用 OID\_PM\_协议\_卸载\_列表 OID 来获取协议卸载的基础的网络适配器上设置的列表。

每个[ **NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构在列表中，NDIS 集**NextProtocolOffloadOffset**从 OID 信息缓冲区开头的偏移量的成员 (即，缓冲区开头的**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构指向) 到下一步 NDIS 开头\_PM\_协议\_卸载结构列表中的。 中的偏移量**NextProtocolOffloadOffset**列表中的最后一个结构的成员为零。

如果网络适配器设置无协议卸载，请设置 NDIS**数据。查询\_信息。BytesWritten**成员的 NDIS\_OID\_为零，并返回 NDIS 请求结构\_状态\_成功。 中的数据**数据。查询\_INFORMATION.InformationBuffer** NDIS 不修改成员。

NDIS 返回请求的以下状态代码之一：

<a href="" id="ndis-status-success"></a>NDIS\_状态\_成功  
请求已成功完成。 **InformationBuffer**如果任何包含的协议卸载列表的指针。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_PENDING  
请求正在等待完成。 最终状态代码和结果将传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_状态\_缓冲区\_过\_短  
信息缓冲区太短。 NDIS 集**数据。查询\_信息。BytesNeeded** NDIS 中的成员\_OID\_结构到最小缓冲区大小的请求是必需的。

<a href="" id="ndis-status-failure"></a>NDIS\_状态\_失败  
请求失败，而原因并非前面的原因。

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
<td><p>支持 NDIS 6.20 及更高版本。 未请求的微型端口驱动程序。 （请参见备注部分。）</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)

 

 




