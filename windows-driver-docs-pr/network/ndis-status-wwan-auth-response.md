---
title: NDIS_STATUS_WWAN_AUTH_RESPONSE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_AUTH_RESPONSE 通知来通知发出使用 OID_WWAN_AUTH_CHALLENGE 查询请求的前一个质询请求接收的质询响应 MB 服务。NDIS_WWAN_AUTH_RESPONSE 结构。
ms.assetid: 24831764-4F6D-481B-A440-4F9CAE1F7501
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_AUTH_RESPONSE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c349fad7075286e8ab2c144b6e0d9801d3a7131a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382663"
---
# <a name="ndisstatuswwanauthresponse"></a>NDIS\_状态\_WWAN\_身份验证\_响应


微型端口驱动程序使用 NDIS\_状态\_WWAN\_身份验证\_响应通知，以通知使用颁发的前一个质询请求接收的质询响应 MB 服务[OID\_WWAN\_身份验证\_质询](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-auth-challenge)查询请求。

微型端口驱动程序还可以发送未经请求的事件与该通知。

使用此 NDIS 状态通知[NDIS\_WWAN\_身份验证\_响应](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_response)结构。

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
<td><p>支持从 Windows 8 开始。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID\_WWAN\_身份验证\_质询](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-auth-challenge)

[NDIS\_WWAN\_AUTH\_RESPONSE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_auth_response)

 

 




