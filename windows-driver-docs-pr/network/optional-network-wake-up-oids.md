---
title: 可选网络唤醒 OID
description: 可选网络唤醒 OID
ms.assetid: 0e9b4844-1623-4bfd-8e73-ebbd970c7e95
keywords:
- 可选的网络唤醒 Oid
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ce2422317338729fccbca0920664bbb9d938449
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366564"
---
# <a name="optional-network-wake-up-oids"></a>可选网络唤醒 OID





若要支持网络唤醒的事件，远程 NDIS 设备必须此外支持[OID\_PNP\_启用\_唤醒\_向上](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-enable-wake-up)由这两种网络协议 (TCP/IP) 的 OID和 NDIS 以启用唤醒功能。 此外下, 表中列出的选项都可用于启用特定类型的模式唤醒。 有关更多详细信息，请参阅 Microsoft Windows 2000 驱动程序开发工具包 (DDK)。

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
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-enable-wake-up" data-raw-source="[OID_PNP_ENABLE_WAKE_UP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-enable-wake-up)">OID_PNP_ENABLE_WAKE_UP</a></p></td>
<td align="left"><p>远程 NDIS 设备唤醒功能，还可以启用</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-add-wake-up-pattern" data-raw-source="[OID_PNP_ADD_WAKE_UP_PATTERN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-add-wake-up-pattern)">OID_PNP_ADD_WAKE_UP_PATTERN</a></p></td>
<td align="left"><p>远程 NDIS 微型端口驱动程序应加载到设备的唤醒模式</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-remove-wake-up-pattern" data-raw-source="[OID_PNP_REMOVE_WAKE_UP_PATTERN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-remove-wake-up-pattern)">OID_PNP_REMOVE_WAKE_UP_PATTERN</a></p></td>
<td align="left"><p>远程 NDIS 微型端口驱动程序应从设备中删除唤醒模式</p></td>
</tr>
</tbody>
</table>

 

 

 





