---
title: OID_WWAN_PIN_EX
description: OID_WWAN_PIN_EX 设置或返回与个人标识号（Pin）相关的扩展信息。
ms.assetid: 4D3D91B2-7B3C-4C8F-B98F-0F9999D04C03
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_PIN_EX 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7dbdb72698f8f5899714aea4972560810dabb287
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843820"
---
# <a name="oid_wwan_pin_ex"></a>OID\_WWAN\_PIN\_EX


OID\_WWAN\_PIN\_EX 集或返回与个人标识号（Pin）相关的扩展信息。

微型端口驱动程序必须异步处理集和查询请求，最初返回 NDIS\_状态\_指示\_需要原始请求，稍后将[**ndis\_状态\_WWAN\_PIN 发送\_信息**](ndis-status-wwan-pin-info.md)状态通知完成了设置或查询请求。

微型端口驱动程序应将[**ndis\_状态发送\_WWAN\_PIN\_信息**](ndis-status-wwan-pin-info.md)状态通知，其中包含[**NDIS\_WWAN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)\_信息，主要用于指示在完成查询请求时是否需要 PIN 来解锁 MB 设备或订户标识模块（SIM 卡）。

请求设置与 Pin 相关的信息的调用方提供[**NDIS\_WWAN\_集\_pin 将\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin_ex)结构发送到微型端口驱动程序，以便将 pin 发送到 MB 设备，启用或禁用 pin 设置，或者更改 SIM 上的 pin。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

 

 




