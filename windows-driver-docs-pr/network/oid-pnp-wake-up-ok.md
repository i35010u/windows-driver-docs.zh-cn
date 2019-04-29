---
title: OID_PNP_WAKE_UP_OK
description: OID_PNP_WAKE_UP_OK
ms.assetid: 93389bfe-11b9-4433-8eca-4446f05d01c0
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_WAKE_UP_OK 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ff15bbc04b762a40323f52d90a05394572ca840a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372457"
---
# <a name="oidpnpwakeupok"></a>OID\_PNP\_WAKE\_UP\_OK





可选的 OID\_PNP\_唤醒\_向上\_确定 OID 指示的微型端口驱动程序的 nic 都已终止的有效唤醒 ups 当 NIC 唤醒到有效的模式匹配或幻数据包的响应中的系统，有效的唤醒时发生。

此 OID 的数据类型为 ULONG 值。

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
<td><p>Version</p></td>
<td><p>NDIS 5.1 和 NDIS 6.0 及更高版本支持。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

 

 




