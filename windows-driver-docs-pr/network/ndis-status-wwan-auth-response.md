---
title: NDIS_STATUS_WWAN_AUTH_RESPONSE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_AUTH_RESPONSE 通知来通知 MB 服务从以前的质询请求收到的质询响应使用 OID_WWAN_AUTH_CHALLENGE 查询请求。NDIS_WWAN_AUTH_RESPONSE 结构。
ms.assetid: 24831764-4F6D-481B-A440-4F9CAE1F7501
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_AUTH_RESPONSE 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4697b98626621dbdce16eb744a501e11e17ea8ea
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844654"
---
# <a name="ndis_status_wwan_auth_response"></a>\_WWAN\_身份验证\_响应的 NDIS\_状态


小型端口驱动程序使用 NDIS\_状态\_WWAN\_AUTH\_响应通知，通知 MB 服务从以前的质询请求收到的质询响应， [\_WWAN\_AUTH\_质询](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-auth-challenge)查询请求。

小型端口驱动程序还可以通过此通知发送未经请求的事件。

此 NDIS 状态通知使用[ndis\_WWAN\_AUTH\_响应](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_response)结构。

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

## <a name="see-also"></a>另请参阅


[OID\_WWAN\_身份验证\_质询](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-auth-challenge)

[NDIS\_WWAN\_身份验证\_响应](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_response)

 

 




