---
title: OID_PNP_REMOVE_WAKE_UP_PATTERN
description: OID_PNP_REMOVE_WAKE_UP_PATTERN
ms.assetid: 493019d0-9cd9-4712-8d18-5ee0264be9e1
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_REMOVE_WAKE_UP_PATTERN 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 171a27315d3b488cff94bb2974905b7584c9cb30
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844037"
---
# <a name="oid_pnp_remove_wake_up_pattern"></a>OID\_PNP\_删除\_唤醒\_向上\_模式





OID\_PNP\_删除\_唤醒\_向上\_模式 OID 请求微型端口驱动程序，以删除以前在 OID 中收到的唤醒模式[\_PNP\_添加\_唤醒\_\_模式](oid-pnp-add-wake-up-pattern.md)请求。 唤醒模式及其掩码由[**NDIS\_PM\_数据包\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)结构进行描述。

[ **\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含以下内容：

-   [**NDIS\_PM\_数据包\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)结构，该结构提供有关该模式及其掩码的信息。

-   一个掩码，用于指示应将传入数据包的哪些字节与模式中的相应字节进行比较。 掩码以数据包的第一个字节开始。 掩码紧跟在**InformationBuffer**中的[**NDIS\_PM\_数据包\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)结构。

-   唤醒模式，从**InformationBuffer**的开头开始**PatternOffset**字节。

在其中，上边缘接收此 OID 请求的中间驱动程序必须始终通过调用 Ndis （Co）请求将请求传播到基础微型端口驱动程序。

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
<td><p>在 NDIS 6.0 和6.1 中受支持。 对于 NDIS 6.20 和更高版本，请改用<a href="oid-pm-remove-wol-pattern.md" data-raw-source="[OID_PM_REMOVE_WOL_PATTERN](oid-pm-remove-wol-pattern.md)">OID_PM_REMOVE_WOL_PATTERN</a> 。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_PM\_数据包\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)

[OID\_PNP\_添加\_唤醒\_向上\_模式](oid-pnp-add-wake-up-pattern.md)

[OID\_PM\_删除\_WOL\_模式](oid-pm-remove-wol-pattern.md)

 

 




