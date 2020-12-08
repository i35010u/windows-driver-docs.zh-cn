---
title: OID_PNP_WAKE_UP_OK
description: OID_PNP_WAKE_UP_OK
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_WAKE_UP_OK 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2fd11d1323137b298a63a6a41b3766567d442389
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827519"
---
# <a name="oid_pnp_wake_up_ok"></a>OID \_ PNP \_ 唤醒 \_ 正常 \_





可选 OID \_ PNP \_ 唤醒 \_ \_ 正常 oid 指示微型端口驱动程序的 NIC 发出信号的有效唤醒的数目。 当 NIC 唤醒系统以响应有效的模式匹配或幻数据包时，会发生有效的唤醒。

此 OID 的数据类型是 ULONG 值。

在其中，上边缘接收此 OID 请求的中间驱动程序必须始终通过调用 Ndis (Co) 请求将请求传播到基础微型端口驱动程序。

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
<td><p>支持 NDIS 5.1 和 NDIS 6.0 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

 

 




