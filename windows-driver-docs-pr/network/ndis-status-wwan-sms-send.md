---
title: NDIS_STATUS_WWAN_SMS_SEND
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SMS_SEND 通知来通知关于完成的上一个发送请求通过 OID_WWAN_SMS_SEND MB 服务。
ms.assetid: f750b09c-1a7c-40d8-8a4e-a7f9f3160248
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SMS_SEND 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0260d8c2314694341098c0960f82d4f163f2ea1f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567307"
---
# <a name="ndisstatuswwansmssend"></a>NDIS\_状态\_WWAN\_SMS\_发送


微型端口驱动程序使用 NDIS\_状态\_WWAN\_SMS\_发送通知来通知关于完成的上一个发送请求通过 MB 服务[OID\_WWAN\_短信\_发送](oid-wwan-sms-send.md)。

微型端口驱动程序不能使用此通知将发送未经请求的事件。

使用此通知[ **NDIS\_WWAN\_SMS\_发送\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567944)结构。

<a name="remarks"></a>备注
-------

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
<td><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID\_WWAN\_SMS\_SEND](oid-wwan-sms-send.md)

[**NDIS\_WWAN\_SMS\_SEND\_STATUS**](https://msdn.microsoft.com/library/windows/hardware/ff567944)

 

 




