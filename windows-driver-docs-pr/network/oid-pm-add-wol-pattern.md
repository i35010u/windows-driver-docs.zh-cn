---
title: OID_PM_ADD_WOL_PATTERN
description: 作为集，NDIS 协议驱动程序使用 OID_PM_ADD_WOL_PATTERN OID 将 LAN 唤醒模式添加到网络适配器。 NDIS_OID_REQUEST 结构的 InformationBuffer 成员包含指向 NDIS_PM_WOL_PATTERN 结构的指针。
ms.assetid: 1005cebb-8ead-4d16-b3ea-5a74da0b054f
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PM_ADD_WOL_PATTERN 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6b3b9c374da2a89a2260fb72f6b766afdbecf935
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844061"
---
# <a name="oid_pm_add_wol_pattern"></a>OID\_PM\_添加\_WOL\_模式


作为集，NDIS 协议驱动程序使用 OID\_PM\_添加\_WOL\_模式 OID，将 LAN 唤醒模式添加到网络适配器。 [**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含指向[**NDIS\_PM\_WOL\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)结构的指针。

<a name="remarks"></a>备注
-------

NDIS 6.20 和更高版本的协议驱动程序使用 OID\_PM\_添加\_WOL\_模式，将 LAN 唤醒（WOL）模式添加到网络适配器。 OID 请求包含一些条件，当网络适配器处于低功耗状态时，它必须与传入数据包进行比较。 网络适配器在收到与模式条件匹配的数据包时必须生成唤醒事件。

协议驱动程序在成功绑定到基础网络适配器后，可以添加 WOL 模式，并且只要它具有必要的数据（如接口的 IP 地址）即可设置 WOL 模式。 协议驱动程序还可以添加 WOL 模式来响应某些其他电源管理事件通知，如拒绝以前添加的 WOL 模式或卸载的协议。

若要避免 NDIS 中的争用条件以及绑定到同一个微型端口适配器的其他协议驱动程序，在 NDIS 开始将网络适配器设置为低功率状态后，将无法在该网络适配器上添加新的唤醒模式的任何尝试。 例如，如果 NDIS 协议驱动程序尝试在处理该网络适配器的**NetEventSetPower**事件通知的上下文中添加新的 WOL 模式，则 ndis 将导致请求失败。

在 NDIS 将此 OID 请求发送到基础 NDIS 驱动程序或完成对过量驱动程序的请求之前，它会将 NDIS\_PM 的 ULONG **PatternId**成员设置[ **\_WOL\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)结构设置为唯一值。 协议驱动程序和 NDIS 将此模式标识符与[OID\_PM 一起使用\_删除\_WOL\_模式](oid-pm-remove-wol-pattern.md)OID 请求，以从基础网络适配器中删除 wol 模式。

**请注意**  模式标识符是网络适配器上设置的每个模式的唯一值。 但是，所有微型端口适配器的模式标识符不是全局唯一的。

 

如果 NDIS 或基础网络适配器删除 WOL 模式，则它将生成[**NDIS\_状态\_PM\_WOL\_模式\_拒绝**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wol-pattern-rejected)的状态指示。 [**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含被拒绝的 WOL 模式的 ULONG wol 模式标识符。

微型端口驱动程序为请求返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>成功的 NDIS\_状态\_  
已成功添加请求的模式。 NDIS\_PM\_WOL\_模式结构中的**PatternId**成员包含模式标识符。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_挂起  
请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-pm-wol-pattern-list-full"></a>NDIS\_状态\_PM\_WOL\_模式\_完全\_  
请求失败，因为模式列表已满，网络适配器无法添加另一种模式。

<a href="" id="ndis-status-resources"></a>NDIS\_状态\_资源  
由于缺少资源，NDIS 或基础网络适配器无法添加新模式。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_状态\_无效\_参数  
NDIS\_PM\_WOL\_模式结构中的一个或多个参数无效。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_状态\_缓存\_\_太短  
信息缓冲区太短。 NDIS 设置**数据。设置\_信息。** \_OID 中的 BytesNeeded 成员\_请求结构到所需的最小缓冲区大小。

<a href="" id="ndis-status-not-supported"></a>不\_支持 NDIS\_状态\_  
网络适配器不支持请求的 WOL 模式。

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

[**NDIS\_PM\_WOL\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_状态\_PM\_WOL\_模式\_被拒绝**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wol-pattern-rejected)

[OID\_PM\_删除\_WOL\_模式](oid-pm-remove-wol-pattern.md)

[OID\_PNP\_添加\_唤醒\_向上\_模式](oid-pnp-add-wake-up-pattern.md)

 

 




