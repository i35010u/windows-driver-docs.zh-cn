---
title: OID_PNP_ENABLE_WAKE_UP
description: OID_PNP_ENABLE_WAKE_UP
ms.assetid: 9afe774b-a429-413f-a7b6-3a3d79d2b95f
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_ENABLE_WAKE_UP 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6d9b3de8297e6b9c001a7014356d3819119841a1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844040"
---
# <a name="oid_pnp_enable_wake_up"></a>OID\_PNP\_启用\_唤醒\_





作为集，OID\_PNP\_启用\_唤醒\_UP OID 指定微型端口驱动程序应在网络适配器中启用的唤醒功能。

作为查询，OID\_PNP\_启用\_唤醒\_获取为网络适配器启用的当前唤醒功能。

[ **\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员是可用于启用唤醒事件组合的标志的位掩码：

<a href="" id="ndis-pnp-wake-up-magic-packet"></a>**NDIS\_PNP\_唤醒\_\_幻\_数据包**  
如果设置，则指定微型端口驱动程序应该允许网络适配器在收到幻数据包时发出唤醒事件。 （*幻数据包*是包含接收网络适配器的以太网地址的16个连续副本的数据包。）如果清除此项，则指定微型端口驱动程序应禁止网络适配器发出此类唤醒事件的信号。

<a href="" id="ndis-pnp-wake-up-pattern-match"></a>**NDIS\_PNP\_唤醒\_\_模式\_匹配**  
如果设置此设置，则指定微型端口驱动程序应启用网络适配器，以便在收到包含协议指定模式的数据包时发出唤醒事件， [\_PNP\_添加\_唤醒\_向上\_模式](oid-pnp-add-wake-up-pattern.md). 如果清除此项，则指定微型端口驱动程序应禁止网络适配器发出此类唤醒事件的信号。

<a href="" id="ndis-pnp-wake-up-link-change"></a>**NDIS\_PNP\_唤醒\_\_链接\_更改**  
保留。 NDIS 忽略此标志。

协议驱动程序使用 NDIS 中网络适配器的唤醒功能[ **\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)，以启用关联网络适配器的唤醒功能。 协议驱动程序还可以查询此 OID，以确定为网络适配器启用了哪些唤醒功能。

NDIS 不会立即启用协议驱动程序指定的唤醒功能。 相反，NDIS 将跟踪启用了协议驱动程序的唤醒功能，刚好在网络适配器转换到低功耗状态之前，NDIS 会将 OID 发送\_PNP\_启用\_唤醒\_将请求发送到微型端口驱动程序，用于启用适当的唤醒事件。

在网络适配器转换到低功耗状态之前（即，在 NDIS 向小型驱动程序发送了[oid\_PNP\_集\_电源](oid-pnp-set-power.md)请求）之前，NDIS 会将微型端口驱动程序发送 OID\_PNP\_启用\_唤醒\_启用适当唤醒功能的请求。

微型端口驱动程序必须执行相应的设备相关步骤，以便在网络适配器上启用或禁用唤醒事件。

微型端口驱动程序应清除使用 OID\_PNP 设置的唤醒功能\_在系统恢复时启用\_唤醒\_。 唤醒功能不应在恢复期间保持。 如果启用了唤醒功能，NDIS 会显式地\_PNP\_启用\_唤醒\_，然后在微型端口转换到低功耗状态。

在其中，上边缘接收此 OID 请求的中间驱动程序必须始终通过调用[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)或[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)函数将该请求传播到基础微型端口驱动程序。

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
<td><p>在 NDIS 6.0 和6.1 中受支持。 对于 NDIS 6.20 和更高版本，请改用<a href="oid-pm-parameters.md" data-raw-source="[OID_PM_PARAMETERS](oid-pm-parameters.md)">OID_PM_PARAMETERS</a> ）。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[ **\_绑定\_参数的 NDIS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)

[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)

[OID\_PM\_参数](oid-pm-parameters.md)

[OID\_PNP\_添加\_唤醒\_向上\_模式](oid-pnp-add-wake-up-pattern.md)

 

 




