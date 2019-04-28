---
title: 设置 CoNDIS WAN 微型端口驱动程序信息
description: 设置 CoNDIS WAN 微型端口驱动程序信息
ms.assetid: 950cb2cb-7f02-4f3c-924a-0d1e7bb19b55
keywords:
- WAN 的 CoNDIS 驱动程序 WDK 网络，信息设置
- OID_WAN_CO_SET_LINK_INFO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ae3a27bae1767e10445859090f81b00f6cf61b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346693"
---
# <a name="setting-condis-wan-miniport-driver-information"></a>设置 CoNDIS WAN 微型端口驱动程序信息





本主题概述了有关的 CoNDIS WAN 的微型端口驱动程序中的设置信息的要求。 上层驱动程序调用[ **NdisCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff561711)与 set 请求更改的 CoNDIS WAN 的微型端口驱动程序和微型端口驱动程序的 NIC 维护的信息。

NDIS NDISWAN 中间驱动程序将转发集请求后，调用 WAN 微型端口驱动程序[ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)函数。 此函数在 CoNDIS WAN 的微型端口驱动程序，是相同的 CoNDIS 任何微型端口驱动程序，不同之处在于 CoNDIS WAN 微型端口驱动程序支持[CoNDIS WAN 对象](https://msdn.microsoft.com/library/windows/hardware/ff545146)。

当前的集请求完成之前，没有其他请求将提交到 WAN 的 CoNDIS 微型端口驱动程序。 如果微型端口驱动程序不会立即完成集请求，它将返回 NDIS\_状态\_从 PENDING *MiniportCoOidRequest*且更高版本调用[ **NdisCoOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff561716)来完成该请求。

CoNDIS WAN 的微型端口驱动程序必须识别并正确应对以下的 CoNDIS WAN Oid。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">名称</th>
<th align="left">可选或必需</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p></p>
<a href="https://msdn.microsoft.com/library/windows/hardware/ff569822" data-raw-source="[OID_WAN_CO_SET_LINK_INFO](https://msdn.microsoft.com/library/windows/hardware/ff569822)">OID_WAN_CO_SET_LINK_INFO</a>为 VC 设置信息。</td>
<td align="left"><p>必需</p></td>
</tr>
</tbody>
</table>

 

CoNDIS WAN 的微型端口驱动程序还支持 NDIS[常规对象](https://msdn.microsoft.com/library/windows/hardware/ff546510)。 若要了解有关的 CoNDIS 微型端口驱动程序中设置信息的详细信息，请参阅[查询或设置信息](querying-or-setting-information.md)。

 

 





