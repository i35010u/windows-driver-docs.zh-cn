---
title: OID_WWAN_PIN_EX
description: OID_WWAN_PIN_EX 设置或返回与个人标识号 (Pin) 相关的扩展的信息。
ms.assetid: 4D3D91B2-7B3C-4C8F-B98F-0F9999D04C03
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_PIN_EX 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5690bd936de7c1cf7dd74205d5713c9779b015dc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522350"
---
# <a name="oidwwanpinex"></a>OID\_WWAN\_PIN\_EX


OID\_WWAN\_PIN\_EX 设置或返回与个人标识号 (Pin) 相关的扩展的信息。

微型端口驱动程序必须处理集和查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_PIN\_信息**](ndis-status-wwan-pin-info.md)状态通知时他们已完成的集或查询请求。

微型端口驱动程序应发送[ **NDIS\_状态\_WWAN\_PIN\_信息**](ndis-status-wwan-pin-info.md)状态通知包含[ **NDIS\_WWAN\_PIN\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567911)结构返回固定类型和 PIN 输入状态的信息，主要用于指示是否需要 PIN 来解锁的 MB 设备或订阅服务器识别模块 （SIM 卡） 完成查询请求时。

调用方请求设置 Pin 与相关的信息提供[ **NDIS\_WWAN\_设置\_PIN\_EX** ](https://msdn.microsoft.com/library/windows/hardware/hh439842)到微型端口驱动程序的结构将 PIN 发送到 MB 设备，可以启用或禁用 PIN 设置，或更改在 sim 卡 PIN。

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
<td><p>版本：支持 Windows 8 和更高版本的 Windows 中。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

 

 




