---
title: OID_PNP_ENABLE_WAKE_UP
description: OID_PNP_ENABLE_WAKE_UP
ms.assetid: 9afe774b-a429-413f-a7b6-3a3d79d2b95f
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_ENABLE_WAKE_UP 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 02f743acd89ff71fdb8a841da1cba8cf4863a972
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213345"
---
# <a name="oid_pnp_enable_wake_up"></a>OID \_ PNP \_ 启用 \_ 唤醒 \_





作为集，OID \_ PNP \_ 启用 \_ 唤醒 \_ OID 指定微型端口驱动程序应在网络适配器中启用的唤醒功能。

作为查询，OID \_ PNP \_ ENABLE \_ 唤醒 \_ 获取为网络适配器启用的当前唤醒功能。

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员是可用于启用唤醒事件组合的标志的位掩码：

<a href="" id="ndis-pnp-wake-up-magic-packet"></a>**NDIS \_ PNP \_ 唤醒 \_ \_ 幻 \_ 数据包**  
如果设置，则指定微型端口驱动程序应该允许网络适配器在收到幻数据包时发出唤醒事件。  (*幻数据包* 是包含接收网络适配器的以太网地址的16个连续副本的数据包 ) 。如果清除此项，则表示微型端口驱动程序应禁止网络适配器发出此类唤醒事件的信号。

<a href="" id="ndis-pnp-wake-up-pattern-match"></a>**NDIS \_ PNP \_ 唤醒 \_ \_ 模式 \_ 匹配**  
如果设置此设置，则指定微型端口驱动程序应允许网络适配器在收到包含协议所指定模式（具有 [OID \_ PNP \_ 添加 \_ 唤醒 \_ \_ 模式](oid-pnp-add-wake-up-pattern.md)）的数据包时，通知唤醒事件。 如果清除此项，则指定微型端口驱动程序应禁止网络适配器发出此类唤醒事件的信号。

<a href="" id="ndis-pnp-wake-up-link-change"></a>**NDIS \_ PNP \_ 唤醒 \_ \_ 链接 \_ 更改**  
保留。 NDIS 忽略此标志。

协议驱动程序使用 [**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters) 中的网络适配器的唤醒功能，以启用关联网络适配器的唤醒功能。 协议驱动程序还可以查询此 OID，以确定为网络适配器启用了哪些唤醒功能。

NDIS 不会立即启用协议驱动程序指定的唤醒功能。 相反，NDIS 将跟踪启用了协议驱动程序的唤醒功能，刚好在网络适配器转换到低功耗状态之前，NDIS 会将 OID \_ PNP \_ 启用 \_ 唤醒 \_ 集请求发送到微型端口驱动程序，以启用适当的唤醒事件。

在网络适配器转换到低功耗状态之前 (也就是说，在 NDIS 发送微型端口驱动程序) [oid \_ pnp \_ 集 \_ 电源](oid-pnp-set-power.md) 请求之前，ndis 将发送微型端口驱动程序 oid \_ pnp \_ enable \_ 唤醒请求， \_ 以启用适当的唤醒功能。

微型端口驱动程序必须执行相应的设备相关步骤，以便在网络适配器上启用或禁用唤醒事件。

微型端口驱动程序应清除使用 OID PNP 设置的唤醒功能，以便 \_ \_ \_ \_ 在系统恢复时唤醒。 唤醒功能不应在恢复期间保持。 如果启用了唤醒功能，NDIS 将在 \_ \_ \_ \_ 微型端口转换到低功耗状态之前，显式设置 OID PNP 启用唤醒。

在其中，上边缘接收此 OID 请求的中间驱动程序必须始终通过调用 [**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest) 或 [**NdisCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest) 函数将该请求传播到基础微型端口驱动程序。

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
<td><p>在 NDIS 6.0 和6.1 中受支持。 对于 NDIS 6.20 和更高版本，请改用 <a href="oid-pm-parameters.md" data-raw-source="[OID_PM_PARAMETERS](oid-pm-parameters.md)">OID_PM_PARAMETERS</a>) 。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NdisCoOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscooidrequest)

[**NdisOidRequest**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)

[OID \_ PM \_ 参数](oid-pm-parameters.md)

[OID \_ PNP \_ 添加 \_ 唤醒 \_ \_ 模式](oid-pnp-add-wake-up-pattern.md)

 

