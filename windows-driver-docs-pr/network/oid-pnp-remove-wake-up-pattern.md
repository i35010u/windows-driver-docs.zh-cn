---
title: OID_PNP_REMOVE_WAKE_UP_PATTERN
description: OID_PNP_REMOVE_WAKE_UP_PATTERN
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_REMOVE_WAKE_UP_PATTERN 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d3a6334838bf3dbf3318c6b7aa449c20bf34b955
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827535"
---
# <a name="oid_pnp_remove_wake_up_pattern"></a>OID \_ PNP \_ 删除 \_ 唤醒 \_ \_ 模式





OID \_ pnp \_ 删除 \_ 唤醒 \_ \_ 模式 OID 请求微型端口驱动程序删除之前在 [OID \_ PNP \_ 添加 \_ 唤醒 \_ \_ 模式](oid-pnp-add-wake-up-pattern.md) 请求中收到的唤醒模式。 唤醒模式连同其掩码，由 [**NDIS \_ PM \_ 数据包 \_ 模式**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern) 结构描述。

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含以下内容：

-   提供有关模式及其掩码的信息的 [**NDIS \_ PM \_ 包 \_ 模式**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern) 结构。

-   一个掩码，用于指示应将传入数据包的哪些字节与模式中的相应字节进行比较。 掩码以数据包的第一个字节开始。 掩码紧跟 **InformationBuffer** 中的 [**NDIS \_ PM \_ 数据包 \_ 模式**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)结构。

-   唤醒模式，从 **InformationBuffer** 的开头开始 **PatternOffset** 字节。

在其中，上边缘接收此 OID 请求的中间驱动程序必须始终通过调用 Ndis (Co) 请求将请求传播到基础微型端口驱动程序。

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
<td><p>在 NDIS 6.0 和6.1 中受支持。 对于 NDIS 6.20 和更高版本，请改用 <a href="oid-pm-remove-wol-pattern.md" data-raw-source="[OID_PM_REMOVE_WOL_PATTERN](oid-pm-remove-wol-pattern.md)">OID_PM_REMOVE_WOL_PATTERN</a> 。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ PM \_ 数据包 \_ 模式**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)

[OID \_ PNP \_ 添加 \_ 唤醒 \_ \_ 模式](oid-pnp-add-wake-up-pattern.md)

[OID \_ PM \_ 删除 \_ WOL \_ 模式](oid-pm-remove-wol-pattern.md)

 

