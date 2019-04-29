---
title: 可选网络唤醒 OID
description: 可选网络唤醒 OID
ms.assetid: 0e9b4844-1623-4bfd-8e73-ebbd970c7e95
keywords:
- 可选的网络唤醒 Oid
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70dff227b8fab5b832dfe5b6f6c5e14990f167a0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359239"
---
# <a name="optional-network-wake-up-oids"></a>可选网络唤醒 OID





若要支持网络唤醒的事件，远程 NDIS 设备必须此外支持[OID\_PNP\_启用\_唤醒\_向上](https://msdn.microsoft.com/library/windows/hardware/ff569775)由这两种网络协议 (TCP/IP) 的 OID和 NDIS 以启用唤醒功能。 此外下, 表中列出的选项都可用于启用特定类型的模式唤醒。 有关更多详细信息，请参阅 Microsoft Windows 2000 驱动程序开发工具包 (DDK)。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569775" data-raw-source="[OID_PNP_ENABLE_WAKE_UP](https://msdn.microsoft.com/library/windows/hardware/ff569775)">OID_PNP_ENABLE_WAKE_UP</a></p></td>
<td align="left"><p>远程 NDIS 设备唤醒功能，还可以启用</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569773" data-raw-source="[OID_PNP_ADD_WAKE_UP_PATTERN](https://msdn.microsoft.com/library/windows/hardware/ff569773)">OID_PNP_ADD_WAKE_UP_PATTERN</a></p></td>
<td align="left"><p>远程 NDIS 微型端口驱动程序应加载到设备的唤醒模式</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569779" data-raw-source="[OID_PNP_REMOVE_WAKE_UP_PATTERN](https://msdn.microsoft.com/library/windows/hardware/ff569779)">OID_PNP_REMOVE_WAKE_UP_PATTERN</a></p></td>
<td align="left"><p>远程 NDIS 微型端口驱动程序应从设备中删除唤醒模式</p></td>
</tr>
</tbody>
</table>

 

 

 





