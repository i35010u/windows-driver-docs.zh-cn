---
title: OID_PNP_ADD_WAKE_UP_PATTERN
description: OID_PNP_ADD_WAKE_UP_PATTERN
ms.assetid: 96b95d1d-d557-4012-b95f-b1c43e2c590f
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_ADD_WAKE_UP_PATTERN 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 41425f07f43e4d8f17747f1ffc98cfa817c6574d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844044"
---
# <a name="oid_pnp_add_wake_up_pattern"></a>OID\_PNP\_添加\_唤醒\_向上\_模式





OID\_PNP\_ADD\_唤醒\_\_将协议驱动程序发送到微型端口驱动程序以指定唤醒模式。 唤醒模式及其掩码由[**NDIS\_PM\_数据包\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)结构进行描述。

一种协议，用于启用微型端口驱动程序的模式匹配唤醒（请参阅[oid\_pnp\_启用\_唤醒\_](oid-pnp-enable-wake-up.md)）使用 OID\_PNP\_添加\_唤醒\_UP\_模式来指定唤醒模式。 唤醒模式可以存储在主机内存或网络适配器上，具体取决于网络适配器的功能。

[ **\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含以下内容：

-   [**NDIS\_PM\_数据包\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)结构，该结构提供有关该模式及其掩码的信息。

-   一个掩码，用于指示应将传入数据包的哪些字节与模式中的相应字节进行比较。 掩码以数据包的第一个字节开始。 掩码紧跟在*InformationBuffer*中的[**NDIS\_PM\_数据包\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)结构。 有关此掩码如何工作的详细信息，请参阅[网络设备类电源管理参考规范](https://go.microsoft.com/fwlink/p/?linkid=27255)。

-   唤醒模式，从*InformationBuffer*的开头开始**PatternOffset**字节。 有关唤醒模式的详细信息，请参阅[网络设备类电源管理参考规范](https://go.microsoft.com/fwlink/p/?linkid=27255)。

微型端口驱动程序可以接受的唤醒模式数可能取决于资源的可用性，例如，小型端口驱动程序为此类模式分配的主机内存或网络适配器中的可用存储。 如果微型端口驱动程序无法添加唤醒模式，原因是资源不足，微型端口驱动程序会返回**NDIS\_状态\_资源**来响应 OID\_PNP\_添加\_唤醒\_UP\_模式。

如果协议驱动程序尝试添加重复模式，微型端口驱动程序应将**NDIS\_状态返回\_无效的\_数据**以响应 OID\_PNP\_\_\_\_模式添加唤醒。

在其中，上边缘接收此 OID 请求的中间驱动程序必须始终通过调用[**NdisRequest**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff554681(v=vs.85))或[**NdisCoRequest**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff551877(v=vs.85))将该请求传播到基础微型端口驱动程序。

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
<td><p>在 NDIS 6.0 和 NDIS 6.1 中受支持。 对于 NDIS 6.20 和更高版本，请改用<a href="oid-pm-add-wol-pattern.md" data-raw-source="[OID_PM_ADD_WOL_PATTERN](oid-pm-add-wol-pattern.md)">OID_PM_ADD_WOL_PATTERN</a> 。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_PM\_数据包\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_packet_pattern)

[OID\_PM\_添加\_WOL\_模式](oid-pm-add-wol-pattern.md)

 

 




