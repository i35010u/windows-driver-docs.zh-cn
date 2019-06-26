---
title: OID_PNP_WAKE_UP_PATTERN_LIST
description: OID_PNP_WAKE_UP_PATTERN_LIST
ms.assetid: 36e4243f-5df6-4231-b1e3-63fcb2e2ec04
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_WAKE_UP_PATTERN_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 423600aae56ab222fba6139c3eadb0c59d80e1ec
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385240"
---
# <a name="oidpnpwakeuppatternlist"></a>OID\_PNP\_WAKE\_UP\_PATTERN\_LIST





OID\_PNP\_唤醒\_向上\_模式\_协议使用列表 OID 来查询当前为微型端口驱动程序的网络适配器设置唤醒模式的列表。 一种协议指定唤醒模式与[OID\_PNP\_添加\_唤醒\_向上\_模式](oid-pnp-add-wake-up-pattern.md)。

OID\_PNP\_唤醒\_向上\_模式\_列表由 NDIS 而不是微型端口驱动程序。

NDIS 返回到协议的微型端口驱动程序中设置每个唤醒模式说明。 描述每个唤醒模式，以及其掩码[ **NDIS\_PM\_数据包\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)结构。

对于每个唤醒模式中， **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含以下：

-   [ **NDIS\_PM\_数据包\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)结构，它提供有关模式和其掩码的信息。

-   一个掩码，指示应与模式中的相应字节进行比较的传入数据包的字节数。 掩码开头的第一个字节的数据包。 掩码紧随[ **NDIS\_PM\_数据包\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)结构**InformationBuffer**。

-   唤醒模式，其开始**PatternOffset**从一开始的字节**InformationBuffer**。

在其中收到此 OID 请求时的上边缘的中间驱动程序必须始终将对基础微型端口驱动程序的请求传播通过调用 Ndis (Co) 请求。

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
<td><p>在 NDIS 6.0 和 6.1 中受支持。 NDIS 6.20 和更高版本，使用<a href="oid-pm-wol-pattern-list.md" data-raw-source="[OID_PM_WOL_PATTERN_LIST](oid-pm-wol-pattern-list.md)">OID_PM_WOL_PATTERN_LIST</a>相反。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_PM\_PACKET\_PATTERN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)

[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[OID\_PM\_WOL\_PATTERN\_LIST](oid-pm-wol-pattern-list.md)

[OID\_PNP\_ADD\_WAKE\_UP\_PATTERN](oid-pnp-add-wake-up-pattern.md)

[OID\_PNP\_REMOVE\_WAKE\_UP\_PATTERN](oid-pnp-remove-wake-up-pattern.md)

 

 




