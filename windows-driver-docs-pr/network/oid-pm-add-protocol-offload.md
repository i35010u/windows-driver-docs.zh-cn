---
title: OID_PM_ADD_PROTOCOL_OFFLOAD
description: 作为一组，NDIS 协议驱动程序使用 OID_PM_ADD_PROTOCOL_OFFLOAD OID 向网络适配器添加用于电源管理的协议卸载。
ms.assetid: 418f4ce8-64af-4e1e-877a-4cc606f63747
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PM_ADD_PROTOCOL_OFFLOAD 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ed9640d8c1a8c5d8aaad441e3ec578337267508c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213369"
---
# <a name="oid_pm_add_protocol_offload"></a>OID \_ PM \_ 添加 \_ 协议 \_ 卸载


作为一组，NDIS 协议驱动程序使用 OID \_ PM \_ 添加 \_ 协议 \_ 卸载 OID，将用于电源管理的协议卸载添加到网络适配器。 [**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构的指针。

<a name="remarks"></a>备注
-------

NDIS 6.20 和更高版本的协议驱动程序使用 OID \_ PM \_ 添加 \_ 协议 \_ 卸载 OID，将用于电源管理的协议卸载添加到网络适配器。 如果请求成功，则当网络适配器处于低功耗状态时，网络适配器必须为卸载的协议生成并传输必要的响应数据包。

协议驱动程序在成功绑定到基础网络适配器后，可以卸载协议，并在它有必要的数据 (如接口的 IP 地址) 以卸载协议后立即将其卸载。 协议驱动程序还可以卸载协议以响应某些其他电源管理事件通知，如拒绝以前添加的 WOL 模式或卸载的协议。

若要避免 NDIS 中的争用条件以及绑定到相同微型端口适配器的其他协议驱动程序，在 NDIS 开始将网络适配器设置为低功率状态之后，将无法尝试将其他协议卸载到该网络适配器。 例如，如果 NDIS 协议驱动程序尝试在处理该网络适配器的 **NetEventSetPower** 事件通知的上下文中卸载协议，则 ndis 将导致请求失败。

在 NDIS 将此 OID 请求发送到基础 NDIS 驱动程序或完成对过量驱动程序的请求之前，它会将[**NDIS \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构的 ULONG **ProtocolOffloadId**成员设置为唯一值。 协议驱动程序和 NDIS 将此协议卸载标识符与 [OID \_ PM \_ 删除 \_ 协议 \_ 卸载](oid-pm-remove-protocol-offload.md) OID 请求一起使用，以从基础网络适配器中删除协议卸载。

**注意**   协议卸载标识符是网络适配器上设置的每个协议卸载的唯一值。 但是，协议卸载标识符在所有网络适配器之间不是全局唯一的。

 

如果 NDIS 或基础网络适配器拒绝卸载，它将生成 [**NDIS \_ 状态 \_ PM \_ 卸载 \_ 拒绝**](./ndis-status-pm-offload-rejected.md) 的状态指示。 这可能会在 \_ 为 OID 返回 NDIS 状态成功之后发生 \_ 。 [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含被拒绝的协议卸载的 ULONG 协议卸载标识符。

有关本机802.11 无线 LAN 微型端口驱动程序如何使用此 OID 的信息，请参阅 [添加和删除低能耗协议卸载](./adding-and-deleting-low-power-protocol-offloads.md)。

微型端口驱动程序为请求返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>NDIS \_ 状态 \_ 成功  
已成功添加请求的协议卸载。 [**NDIS \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构的**ProtocolOffloadId**成员包含一个协议卸载标识符。

<a href="" id="ndis-status-pending"></a>NDIS \_ 状态 \_ 挂起  
请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-pm-protocol-offload-list-full"></a>NDIS \_ 状态 \_ PM \_ 协议 \_ 卸载 \_ 列表已 \_ 满  
请求失败，因为协议卸载列表已满，网络适配器无法添加另一个协议卸载。

<a href="" id="ndis-status-resources"></a>NDIS \_ 状态 \_ 资源  
由于缺少资源，NDIS 或基础网络适配器无法添加新的协议卸载。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS \_ 状态 \_ 无效 \_ 参数  
[**NDIS \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构中的一个或多个参数无效。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS \_ 状态 \_ 缓冲区 \_ 太 \_ 短  
信息缓冲区太短。 NDIS 设置 **数据。设置 \_ 信息。** 将 NDIS OID 请求结构中的成员 BytesNeeded \_ \_ 为所需的最小缓冲区大小。

<a href="" id="ndis-status-not-supported"></a>\_ \_ 不支持 NDIS \_ 状态  
网络适配器不支持请求的协议卸载。

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
<td><p>版本</p></td>
<td><p>在 NDIS 6.20 和更高版本中受支持。 对于微型端口驱动程序是必需的。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)

[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**已 \_ 拒绝 NDIS 状态 \_ PM \_ 卸载 \_**](./ndis-status-pm-offload-rejected.md)

[OID \_ PM \_ 删除 \_ 协议 \_ 卸载](oid-pm-remove-protocol-offload.md)

[添加和删除低功耗协议卸载](./adding-and-deleting-low-power-protocol-offloads.md)

 

