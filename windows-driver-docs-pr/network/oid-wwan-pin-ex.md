---
title: OID_WWAN_PIN_EX
description: OID_WWAN_PIN_EX 设置或返回与 (Pin) 的个人识别码相关的扩展信息。
ms.assetid: 4D3D91B2-7B3C-4C8F-B98F-0F9999D04C03
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_PIN_EX 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 204a0f72e3ac966d26480f3bba7c7b84b4207776
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209289"
---
# <a name="oid_wwan_pin_ex"></a>OID \_ WWAN \_ PIN （ \_ EX）


OID \_ WWAN \_ PIN \_ EX 设置或返回与)  (Pin 相关的个人识别码相关的扩展信息。

微型端口驱动程序必须异步处理集和查询请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，稍后在完成了 set 或 query 请求后发送 [**ndis \_ 状态 \_ WWAN \_ PIN \_ 信息**](ndis-status-wwan-pin-info.md) 状态通知。

微型端口驱动程序应发送 [**ndis \_ 状态 \_ WWAN \_ pin \_ 信息**](ndis-status-wwan-pin-info.md) 状态通知，其中包含 [**NDIS \_ WWAN \_ pin \_ 信息**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info) 结构来返回 pin 类型和 pin 输入状态信息，主要用于指示在完成查询请求时，是否需要 PIN 来解锁 MB 设备或订户标识模块 (SIM 卡) 。

请求设置与 Pin 相关的信息的调用方向微型端口驱动程序提供 [**NDIS \_ WWAN \_ 集 \_ PIN \_ EX**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin_ex) 结构，以将 pin 发送到 MB 设备，启用或禁用 pin 设置，或者更改 SIM 上的 pin。

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
<td><p>版本：在 windows 8 及更高版本的 Windows 中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

 

