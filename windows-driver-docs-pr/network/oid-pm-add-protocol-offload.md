---
title: OID_PM_ADD_PROTOCOL_OFFLOAD
description: 作为一组，NDIS 协议驱动程序使用 OID_PM_ADD_PROTOCOL_OFFLOAD OID 向网络适配器添加用于电源管理的协议卸载。
ms.assetid: 418f4ce8-64af-4e1e-877a-4cc606f63747
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PM_ADD_PROTOCOL_OFFLOAD 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 71afaee5046ece17be585c6ba55b434577d85db7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844064"
---
# <a name="oid_pm_add_protocol_offload"></a>OID\_PM\_添加\_协议\_卸载


作为一组，NDIS 协议驱动程序使用 OID\_PM\_将\_协议添加\_卸载 OID，以将电源管理的协议卸载添加到网络适配器。 [**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构的指针。

<a name="remarks"></a>备注
-------

NDIS 6.20 和更高版本的协议驱动程序使用 OID\_PM\_将\_协议添加\_卸载 OID，以将电源管理的协议卸载添加到网络适配器。 如果请求成功，则当网络适配器处于低功耗状态时，网络适配器必须为卸载的协议生成并传输必要的响应数据包。

协议驱动程序在成功绑定到基础网络适配器后，可以卸载协议，并在它具有必要的数据（如接口的 IP 地址）时立即卸载协议。 协议驱动程序还可以卸载协议以响应某些其他电源管理事件通知，如拒绝以前添加的 WOL 模式或卸载的协议。

若要避免 NDIS 中的争用条件以及绑定到相同微型端口适配器的其他协议驱动程序，在 NDIS 开始将网络适配器设置为低功率状态之后，将无法尝试将其他协议卸载到该网络适配器。 例如，如果 NDIS 协议驱动程序尝试在处理该网络适配器的**NetEventSetPower**事件通知的上下文中卸载协议，则 ndis 将导致请求失败。

在 NDIS 将此 OID 请求发送到基础 NDIS 驱动程序或完成对过量驱动程序的请求之前，它会将[**NDIS\_PM\_协议**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)的 ULONG **ProtocolOffloadId**成员设置为唯一值\_卸载结构。 协议驱动程序和 NDIS 将此协议卸载标识符与[OID\_PM 一起使用\_删除\_协议\_卸载](oid-pm-remove-protocol-offload.md)OID 请求，以从基础网络适配器中删除协议卸载。

**请注意**  协议卸载标识符是网络适配器上设置的每个协议卸载的唯一值。 但是，协议卸载标识符在所有网络适配器之间不是全局唯一的。

 

如果 NDIS 或基础网络适配器拒绝卸载，它将生成[**NDIS\_状态\_PM\_卸载\_拒绝**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-offload-rejected)的状态指示。 这可能会在将 NDIS\_状态返回到 OID\_SUCCESS 后发生。 [**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含被拒绝的协议卸载的 ULONG 协议卸载标识符。

有关本机802.11 无线 LAN 微型端口驱动程序如何使用此 OID 的信息，请参阅[添加和删除低能耗协议卸载](https://docs.microsoft.com/windows-hardware/drivers/network/adding-and-deleting-low-power-protocol-offloads)。

微型端口驱动程序为请求返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>成功的 NDIS\_状态\_  
已成功添加请求的协议卸载。 [**NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构中的**ProtocolOffloadId**成员包含协议卸载标识符。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_挂起  
请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-pm-protocol-offload-list-full"></a>NDIS\_状态\_PM\_协议\_卸载\_完全\_  
请求失败，因为协议卸载列表已满，网络适配器无法添加另一个协议卸载。

<a href="" id="ndis-status-resources"></a>NDIS\_状态\_资源  
由于缺少资源，NDIS 或基础网络适配器无法添加新的协议卸载。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_状态\_无效\_参数  
NDIS\_PM 中的一个或多个参数[ **\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构无效。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_状态\_缓存\_\_太短  
信息缓冲区太短。 NDIS 设置**数据。设置\_信息。** \_OID 中的 BytesNeeded 成员\_请求结构到所需的最小缓冲区大小。

<a href="" id="ndis-status-not-supported"></a>不\_支持 NDIS\_状态\_  
网络适配器不支持请求的协议卸载。

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
<td><p>在 NDIS 6.20 和更高版本中受支持。 对于微型端口驱动程序是必需的。</p></td>
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

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[ **\_PM\_卸载\_拒绝的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-offload-rejected)

[OID\_PM\_删除\_协议\_卸载](oid-pm-remove-protocol-offload.md)

[添加和删除低能耗协议卸载](https://docs.microsoft.com/windows-hardware/drivers/network/adding-and-deleting-low-power-protocol-offloads)

 

 




