---
title: OID_PNP_WAKE_UP_PATTERN_LIST
description: OID_PNP_WAKE_UP_PATTERN_LIST
ms.assetid: 36e4243f-5df6-4231-b1e3-63fcb2e2ec04
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_WAKE_UP_PATTERN_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5fc6dbcef75e41c260d9b08e355e747b2211e793
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844034"
---
# <a name="oid_pnp_wake_up_pattern_list"></a>OID\_PNP\_唤醒\_\_模式\_列表





OID\_PNP\_唤醒\_UP\_模式使用\_列表 OID 来查询当前为微型端口驱动程序网络适配器设置的唤醒模式的列表。 协议指定具有 OID\_PNP 的唤醒模式[\_添加\_唤醒\_向上\_模式](oid-pnp-add-wake-up-pattern.md)。

OID\_PNP\_唤醒\_，\_模式\_列表由 NDIS 而不是微型端口驱动程序处理。

NDIS 返回到协议，其中包含微型端口驱动程序中每个唤醒模式集的说明。 每个唤醒模式连同其掩码，都由[**NDIS\_PM\_数据包\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)结构进行描述。

对于每个唤醒模式， [**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含以下内容：

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
<td><p>在 NDIS 6.0 和6.1 中受支持。 对于 NDIS 6.20 和更高版本，请改用<a href="oid-pm-wol-pattern-list.md" data-raw-source="[OID_PM_WOL_PATTERN_LIST](oid-pm-wol-pattern-list.md)">OID_PM_WOL_PATTERN_LIST</a> 。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_PM\_数据包\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[OID\_PM\_WOL\_模式\_列表](oid-pm-wol-pattern-list.md)

[OID\_PNP\_添加\_唤醒\_向上\_模式](oid-pnp-add-wake-up-pattern.md)

[OID\_PNP\_删除\_唤醒\_向上\_模式](oid-pnp-remove-wake-up-pattern.md)

 

 




