---
title: NDIS_STATUS_WWAN_AUTH_RESPONSE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_AUTH_RESPONSE 通知来通知发出使用 OID_WWAN_AUTH_CHALLENGE 查询请求的前一个质询请求接收的质询响应 MB 服务。NDIS_WWAN_AUTH_RESPONSE 结构。
ms.assetid: 24831764-4F6D-481B-A440-4F9CAE1F7501
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_AUTH_RESPONSE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 40f31d51a25ecbc8f102f4614af3198bbeb37ec3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555956"
---
# <a name="ndisstatuswwanauthresponse"></a>NDIS\_状态\_WWAN\_身份验证\_响应


微型端口驱动程序使用 NDIS\_状态\_WWAN\_身份验证\_响应通知，以通知使用颁发的前一个质询请求接收的质询响应 MB 服务[OID\_WWAN\_身份验证\_质询](https://msdn.microsoft.com/library/windows/hardware/hh440092)查询请求。

微型端口驱动程序还可以发送未经请求的事件与该通知。

使用此 NDIS 状态通知[NDIS\_WWAN\_身份验证\_响应](https://msdn.microsoft.com/library/windows/hardware/hh439834)结构。

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
<td><p>支持从 Windows 8 开始。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_WWAN\_身份验证\_质询](https://msdn.microsoft.com/library/windows/hardware/hh440092)

[NDIS\_WWAN\_AUTH\_RESPONSE](https://msdn.microsoft.com/library/windows/hardware/hh439834)

 

 




