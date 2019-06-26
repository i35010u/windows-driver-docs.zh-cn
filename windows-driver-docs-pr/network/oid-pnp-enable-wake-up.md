---
title: OID_PNP_ENABLE_WAKE_UP
description: OID_PNP_ENABLE_WAKE_UP
ms.assetid: 9afe774b-a429-413f-a7b6-3a3d79d2b95f
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_ENABLE_WAKE_UP 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6f027a8e49ad86fa06830da43de8f26e71ba6d55
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357670"
---
# <a name="oidpnpenablewakeup"></a>OID\_PNP\_启用\_唤醒\_向上





作为一组 OID\_PNP\_启用\_唤醒\_向上 OID 指定网络适配器中的微型端口驱动程序应启用唤醒功能。

为查询，OID\_PNP\_启用\_唤醒\_向上获取网络适配器启用当前唤醒功能。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构是可用于启用组合的标志的位掩码唤醒事件：

<a href="" id="ndis-pnp-wake-up-magic-packet"></a>**NDIS\_PNP\_唤醒\_向上\_MAGIC\_数据包**  
设置时，指定微型端口驱动程序应启用的网络适配器上接收幻数据包唤醒事件发出信号。 (A*幻数据包*是包含 16 个连续副本接收的网络适配器的以太网地址的数据包。)清除时，指定微型端口驱动程序，应禁用网络适配器从信号这种情况下唤醒。

<a href="" id="ndis-pnp-wake-up-pattern-match"></a>**NDIS\_PNP\_唤醒\_向上\_模式\_匹配**  
设置时，指定微型端口驱动程序应启用的网络适配器上接收的数据包，包含通过协议与指定的模式的唤醒事件发出信号[OID\_PNP\_添加\_唤醒\_向上\_模式](oid-pnp-add-wake-up-pattern.md)。 清除时，指定微型端口驱动程序，应禁用网络适配器从信号这种情况下唤醒。

<a href="" id="ndis-pnp-wake-up-link-change"></a>**NDIS\_PNP\_唤醒\_向上\_链接\_更改**  
保留。 NDIS 将忽略此标志。

协议驱动程序使用的网络适配器中的唤醒功能[ **NDIS\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)来启用关联的网络适配器的唤醒功能。 协议驱动程序还可以查询此 OID 确定哪些唤醒功能已启用的网络适配器。

NDIS 不会立即启用协议驱动程序指定的唤醒功能。 相反，NDIS 跟踪协议驱动程序启用了唤醒功能并，只需将网络适配器转换为低功耗状态之前，NDIS 发送 OID\_PNP\_启用\_唤醒\_集对微型端口驱动程序的请求启用相应的唤醒活动。

之前，网络适配器将转换为低功耗状态 (即 NDIS 发送微型端口驱动程序之前[OID\_PNP\_设置\_POWER](oid-pnp-set-power.md)请求)，NDIS 发送 OID微型端口驱动程序\_PNP\_启用\_唤醒\_请求以启用相应的唤醒功能。

微型端口驱动程序必须执行相应的依赖于设备的步骤，以启用或禁用网络适配器上的唤醒事件。

微型端口驱动程序应清除唤醒功能使用 OID 设置 NDIS\_PNP\_启用\_唤醒\_向上何时恢复系统。 不应在简历中保持唤醒功能。 如果启用了唤醒功能，NDIS 显式设置 OID\_PNP\_启用\_唤醒\_向上之前，微型端口将转换为低功耗状态。

在其中收到此 OID 请求时的上边缘的中间驱动程序必须始终将对基础微型端口驱动程序的请求传播通过调用[ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)或[ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)函数。

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
<td><p>在 NDIS 6.0 和 6.1 中受支持。 有关 NDIS 6.20 和更高版本，使用<a href="oid-pm-parameters.md" data-raw-source="[OID_PM_PARAMETERS](oid-pm-parameters.md)">OID_PM_PARAMETERS</a>相反)。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_BIND\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NdisCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)

[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)

[OID\_PM\_PARAMETERS](oid-pm-parameters.md)

[OID\_PNP\_ADD\_WAKE\_UP\_PATTERN](oid-pnp-add-wake-up-pattern.md)

 

 




