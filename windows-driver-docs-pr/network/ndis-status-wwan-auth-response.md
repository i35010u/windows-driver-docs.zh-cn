---
title: NDIS_STATUS_WWAN_AUTH_RESPONSE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_AUTH_RESPONSE 通知来通知 MB 服务：收到的质询响应是使用 OID_WWAN_AUTH_CHALLENGE 查询请求发出的。NDIS_WWAN_AUTH_RESPONSE 结构。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_AUTH_RESPONSE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6b283fb53cf11a73c476f14a6d01aae827e107f4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838415"
---
# <a name="ndis_status_wwan_auth_response"></a>NDIS \_ 状态 \_ WWAN \_ 身份验证 \_ 响应


微型端口驱动程序使用 NDIS \_ 状态 " \_ WWAN \_ 身份验证 \_ 响应通知"，通知 MB 服务从以前的质询请求收到的质询响应使用 [OID \_ WWAN \_ 身份验证 \_ 质询](./oid-wwan-auth-challenge.md) 查询请求。

小型端口驱动程序还可以通过此通知发送未经请求的事件。

此 NDIS 状态通知使用 [ndis \_ WWAN \_ 身份验证 \_ 响应](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_response) 结构。

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
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID \_ WWAN \_ 身份验证 \_ 质询](./oid-wwan-auth-challenge.md)

[NDIS \_ WWAN \_ 身份验证 \_ 响应](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_response)

 

