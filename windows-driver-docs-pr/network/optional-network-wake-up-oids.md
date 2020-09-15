---
title: 可选网络唤醒 OID
description: 可选网络唤醒 OID
ms.assetid: 0e9b4844-1623-4bfd-8e73-ebbd970c7e95
keywords:
- 可选网络唤醒 Oid
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ebb1d150d391ea67022cd55dcecf31998b6f9b2
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104564"
---
# <a name="optional-network-wake-up-oids"></a>可选网络唤醒 OID





若要支持网络唤醒事件，远程 NDIS 设备还必须支持 [OID \_ PNP \_ 启用 \_ \_ ](./oid-pnp-enable-wake-up.md) (tcp/ip) 和 NDIS 的网络协议所使用的唤醒 oid，以实现唤醒功能。 此外，下表中列出的选项可用于启用特定类型的唤醒模式。 有关更多详细信息，请参阅 Microsoft Windows 2000 驱动程序开发工具包 (DDK) 。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">支持</th>
<th align="left">OID</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-pnp-enable-wake-up" data-raw-source="[OID_PNP_ENABLE_WAKE_UP](./oid-pnp-enable-wake-up.md)">OID_PNP_ENABLE_WAKE_UP</a></p></td>
<td align="left"><p>可以启用的远程 NDIS 设备唤醒功能</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-pnp-add-wake-up-pattern" data-raw-source="[OID_PNP_ADD_WAKE_UP_PATTERN](./oid-pnp-add-wake-up-pattern.md)">OID_PNP_ADD_WAKE_UP_PATTERN</a></p></td>
<td align="left"><p>远程 NDIS 微型端口驱动程序应加载到设备的唤醒模式</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-pnp-remove-wake-up-pattern" data-raw-source="[OID_PNP_REMOVE_WAKE_UP_PATTERN](./oid-pnp-remove-wake-up-pattern.md)">OID_PNP_REMOVE_WAKE_UP_PATTERN</a></p></td>
<td align="left"><p>远程 NDIS 微型端口驱动程序应从设备中删除的唤醒模式</p></td>
</tr>
</tbody>
</table>

 

