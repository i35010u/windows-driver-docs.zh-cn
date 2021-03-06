---
title: OID_PM_PROTOCOL_OFFLOAD_LIST
description: 作为查询，过量驱动程序可以使用 OID_PM_PROTOCOL_OFFLOAD_LIST OID 来枚举基础网络适配器上设置的协议卸载。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PM_PROTOCOL_OFFLOAD_LIST 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c148bd868cc5b1cd0028897004db68107aa76d0a
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249015"
---
# <a name="oid_pm_protocol_offload_list"></a>OID \_ PM \_ 协议 \_ 卸载 \_ 列表


作为查询，过量驱动程序可以使用 OID \_ PM \_ 协议 \_ 卸载 \_ 列表 oid 来枚举基础网络适配器上设置的协议卸载。 成功从 OID 查询请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含一个指针，该指针指向描述当前活动的协议 [**卸载的 NDIS \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构的列表。

<a name="remarks"></a>备注
-------

NDIS 处理微型端口驱动程序的查询。 NDIS 驱动程序可以使用 OID \_ PM \_ 协议 \_ 卸载 \_ 列表 OID 获取在基础网络适配器上设置的协议卸载列表。

对于列表中的每个 [**NDIS \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构，ndis 会将 **NextProtocolOffloadOffset** 成员设置为距 OID 信息缓冲区开始处的偏移量， (即， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员指向的缓冲区开始) 到列表中的下一 ndis \_ PM \_ 协议 \_ 卸载结构的开头。 列表中最后一个结构的 **NextProtocolOffloadOffset** 成员中的偏移量为零。

如果未在网络适配器上设置任何协议卸载，NDIS 将设置 **数据。查询 \_ 信息。** 将 ndis \_ OID 请求结构的成员 BytesWritten \_ 为零并返回 ndis \_ 状态 \_ 成功。 数据内的数据 **。\_InformationBuffer** 成员不由 NDIS 修改。

NDIS 为请求返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>NDIS \_ 状态 \_ 成功  
请求已成功完成。 **InformationBuffer** 包含指向协议卸载列表的指针（如果有）。

<a href="" id="ndis-status-pending"></a>NDIS \_ 状态 \_ 挂起  
请求正在等待完成。 最终状态代码和结果将传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS \_ 状态 \_ 缓冲区 \_ 太 \_ 短  
信息缓冲区太短。 NDIS 设置 **数据。查询 \_ 信息。** 将 NDIS OID 请求结构中的成员 BytesNeeded \_ \_ 为所需的最小缓冲区大小。

<a href="" id="ndis-status-failure"></a>NDIS \_ 状态 \_ 故障  
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
<td><p>Version</p></td>
<td><p>在 NDIS 6.20 和更高版本中受支持。 未请求微型端口驱动程序。 （请参见“备注”部分。）</p></td>
</tr>
<tr class="even">
<td><p>标题</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)

 

