---
title: OID_PNP_ADD_WAKE_UP_PATTERN
description: OID_PNP_ADD_WAKE_UP_PATTERN
ms.assetid: 96b95d1d-d557-4012-b95f-b1c43e2c590f
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_ADD_WAKE_UP_PATTERN 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d0868a29a7ad7afd80af101b6a335f197fffd184
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562350"
---
# <a name="oidpnpaddwakeuppattern"></a>OID\_PNP\_ADD\_WAKE\_UP\_PATTERN





OID\_PNP\_添加\_唤醒\_向上\_模式 OID 由发送协议驱动程序微型端口驱动程序以指定唤醒模式。 由描述唤醒模式，以及其掩码[ **NDIS\_PM\_数据包\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff566756)结构。

一种协议，使模式匹配唤醒的微型端口驱动程序 (请参阅[OID\_PNP\_启用\_唤醒\_向上](oid-pnp-enable-wake-up.md)) 使用 OID\_PNP\_添加\_唤醒\_向上\_模式来指定唤醒模式。 可以存储唤醒模式，在主机内存或网络适配器，具体取决于网络适配器的功能上。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含以下：

-   [ **NDIS\_PM\_数据包\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff566756)结构，它提供有关模式和其掩码的信息。

-   一个掩码，指示应与模式中的相应字节进行比较的传入数据包的字节数。 掩码开头的第一个字节的数据包。 掩码紧随[ **NDIS\_PM\_数据包\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff566756)结构*InformationBuffer*。 有关此掩码的工作原理的详细信息，请参阅[网络设备类电源管理的参考规范](https://go.microsoft.com/fwlink/p/?linkid=27255)。

-   唤醒模式，其开始**PatternOffset**从一开始的字节*InformationBuffer*。 有关唤醒模式的详细信息，请参阅[网络设备类电源管理的参考规范](https://go.microsoft.com/fwlink/p/?linkid=27255)。

唤醒模式微型端口驱动程序可以接受从一种协议的数量可能依赖的资源，例如微型端口驱动程序已为此类模式或可用存储的网络适配器分配的主机内存可用性。 如果微型端口驱动程序不能添加唤醒模式由于资源不足，微型端口驱动程序返回**NDIS\_状态\_资源**OID 响应\_PNP\_添加\_唤醒\_向上\_模式。

如果协议驱动程序将尝试添加的重复模式，应返回微型端口驱动程序**NDIS\_状态\_无效\_数据**响应 OID\_PNP\_添加\_唤醒\_向上\_模式。

在其中收到此 OID 请求时的上边缘的中间驱动程序必须始终将对基础微型端口驱动程序的请求传播通过调用[ **NdisRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff554681)或[ **NdisCoRequest**](https://msdn.microsoft.com/library/windows/hardware/ff551877)。

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
<td><p>NDIS 6.0 和 NDIS 6.1 支持。 NDIS 6.20 和更高版本，使用<a href="oid-pm-add-wol-pattern.md" data-raw-source="[OID_PM_ADD_WOL_PATTERN](oid-pm-add-wol-pattern.md)">OID_PM_ADD_WOL_PATTERN</a>相反。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_PM\_PACKET\_PATTERN**](https://msdn.microsoft.com/library/windows/hardware/ff566756)

[OID\_PM\_ADD\_WOL\_PATTERN](oid-pm-add-wol-pattern.md)

 

 




