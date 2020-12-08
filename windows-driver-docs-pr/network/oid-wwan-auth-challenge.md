---
title: OID_WWAN_AUTH_CHALLENGE
description: OID_WWAN_AUTH_CHALLENGE 将身份验证质询发送到 MB 设备或订阅服务器标识模块 (SIM) 卡，以获取来自 SIM 的响应。 n NDIS_STATUS_WWAN_AUTHENTICATION_RESPONSE 状态通知，其中包含 NDIS_WWAN_AUTHENTICATION_RESPONSE 结构，以便在完成查询请求时，根据调用方的质询提供请求的身份验证密钥。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_AUTH_CHALLENGE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6e7e57587ea72b817a1056652a6d390b557e3e0e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797987"
---
# <a name="oid_wwan_auth_challenge"></a>OID \_ WWAN \_ 身份验证 \_ 质询


OID \_ WWAN \_ 身份验证 \_ 质询向 MB 设备或订户标识模块 (sim) 卡发送身份验证质询，以获取来自 sim 的响应。

不支持设置请求。

这是一个可选 OID。 当微型端口驱动程序实现它时，它们必须异步处理查询请求，最初返回 \_ \_ \_ 原始请求所需的 ndis 状态指示，稍后发送 ndis \_ 状态 \_ WWAN \_ 身份验证 \_ 响应状态通知，其中包含 ndis \_ WWAN 身份验证 \_ \_ 响应结构，以根据调用方在完成查询请求时的质询提供请求的身份验证密钥。

<a name="remarks"></a>备注
-------

当处理此 OID 时，微型端口驱动程序可以访问 SIM 卡，但不应访问提供程序网络。 即使在无线电关闭或飞行模式下，此 OID 也必须有效。

OID \_ WWAN \_ 身份验证 \_ 质询同时支持第二代和第三代移动网络。 SIM 指定了一种身份验证机制，该机制基于 GSM 身份验证和密钥协议基元，后者是第二代移动网络标准。 （也称为）使用第三代身份验证和密钥协议机制，为通用移动通信系统 (UMTS) 在 ts 33.102 中指定，在 \[ \] S0055 中为 CDMA2000 指定， \[ \] 具体取决于设备的功能。

如果微型端口驱动程序 \_ 不 \_ \_ 支持返回一种或所有身份验证方法，则它应返回不受支持的 NDIS 状态。

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
<td><p>从 Windows 8 开始支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

 

 




