---
title: OID_PNP_WAKE_UP_ERROR
description: OID_PNP_WAKE_UP_ERROR
ms.assetid: e6386a35-7077-45b3-bc0c-164477168a55
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_WAKE_UP_ERROR 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 49e020892478c0c86c55a916ce53e836801b8bd7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561506"
---
# <a name="oidpnpwakeuperror"></a>OID\_PNP\_WAKE\_UP\_ERROR





可选的 OID\_PNP\_唤醒\_向上\_错误 OID 指示 false 的唤醒 ups 微型端口驱动程序的网络适配器的发送信号的数目。 网络适配器时不应具有唤醒系统时，会发生 false 唤醒。 例如，网络适配器可能会错误地唤醒系统由于不精确的模式匹配。

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
<td><p>版本</p></td>
<td><p>NDIS 5.1 和 NDIS 6.0 及更高版本支持。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

 

 




