---
title: OID_PNP_WAKE_UP_ERROR
description: OID_PNP_WAKE_UP_ERROR
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PNP_WAKE_UP_ERROR 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 807329e2f8dd89311da555fc5103fe702ed11cb6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827525"
---
# <a name="oid_pnp_wake_up_error"></a>OID \_ PNP \_ 唤醒 \_ \_ 错误





可选 OID \_ PNP \_ 唤醒 \_ \_ 错误 OID 指示微型端口驱动程序的网络适配器发出信号的虚假唤醒的数目。 如果网络适配器在不应安装时唤醒系统，则会发生虚假唤醒。 例如，由于模式匹配不精确，网络适配器可能会错误地唤醒系统。

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

 

 




