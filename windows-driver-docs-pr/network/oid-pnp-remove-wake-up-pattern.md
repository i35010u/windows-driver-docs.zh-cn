---
title: OID_PNP_REMOVE_WAKE_UP_PATTERN
description: OID_PNP_REMOVE_WAKE_UP_PATTERN
ms.assetid: 493019d0-9cd9-4712-8d18-5ee0264be9e1
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_REMOVE_WAKE_UP_PATTERN 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a28cc63e48767ddff5d42b388d61f8253c849579
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547876"
---
# <a name="oidpnpremovewakeuppattern"></a>OID\_PNP\_REMOVE\_WAKE\_UP\_PATTERN





OID\_PNP\_删除\_唤醒\_向上\_模式 OID 请求微型端口驱动程序，若要删除它以前接收中的唤醒模式[OID\_PNP\_添加\_唤醒\_向上\_模式](oid-pnp-add-wake-up-pattern.md)请求。 由描述唤醒模式，以及其掩码[ **NDIS\_PM\_数据包\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff566756)结构。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含以下：

-   [ **NDIS\_PM\_数据包\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff566756)结构，它提供有关模式和其掩码的信息。

-   一个掩码，指示应与模式中的相应字节进行比较的传入数据包的字节数。 掩码开头的第一个字节的数据包。 掩码紧随[ **NDIS\_PM\_数据包\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff566756)结构**InformationBuffer**。

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
<td><p>版本</p></td>
<td><p>在 NDIS 6.0 和 6.1 中受支持。 NDIS 6.20 和更高版本，使用<a href="oid-pm-remove-wol-pattern.md" data-raw-source="[OID_PM_REMOVE_WOL_PATTERN](oid-pm-remove-wol-pattern.md)">OID_PM_REMOVE_WOL_PATTERN</a>相反。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_PM\_PACKET\_PATTERN**](https://msdn.microsoft.com/library/windows/hardware/ff566756)

[OID\_PNP\_ADD\_WAKE\_UP\_PATTERN](oid-pnp-add-wake-up-pattern.md)

[OID\_PM\_REMOVE\_WOL\_PATTERN](oid-pm-remove-wol-pattern.md)

 

 




