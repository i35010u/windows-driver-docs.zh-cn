---
title: NDIS_STATUS_WWAN_SMS_SEND
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SMS_SEND 通知通过 OID_WWAN_SMS_SEND 通知 MB 服务完成以前的发送请求。
ms.assetid: f750b09c-1a7c-40d8-8a4e-a7f9f3160248
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SMS_SEND 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6560b76f0fd200fcd796fe5e5521b346253f23ab
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213875"
---
# <a name="ndis_status_wwan_sms_send"></a>NDIS \_ 状态 \_ WWAN \_ 短信 \_ 发送


微型端口驱动程序使用 NDIS \_ 状态 \_ wwan \_ sms \_ 发送通知，通过 [OID \_ WWAN \_ sms \_ send](oid-wwan-sms-send.md)通知 MB 服务完成以前的发送请求。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用 [**NDIS \_ WWAN \_ SMS \_ 发送 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status) 结构。

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
<td><p>在 windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID \_ WWAN \_ SMS \_ 发送](oid-wwan-sms-send.md)

[**NDIS \_ WWAN \_ SMS \_ 发送 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status)

 

