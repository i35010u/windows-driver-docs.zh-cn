---
title: NDIS_STATUS_WWAN_SMS_SEND
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SMS_SEND 通知来通知 MB 服务通过 OID_WWAN_SMS_SEND 完成以前的发送请求。
ms.assetid: f750b09c-1a7c-40d8-8a4e-a7f9f3160248
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SMS_SEND 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 56a8a7cdc44a7d6504202a0214b809b7cde9d486
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844632"
---
# <a name="ndis_status_wwan_sms_send"></a>WWAN\_SMS\_发送\_的 NDIS\_状态


微型端口驱动程序使用 NDIS\_状态\_WWAN\_SMS\_发送通知，通过[OID\_wwan\_SMS\_发送](oid-wwan-sms-send.md)通知 MB 服务完成以前发送请求的完成。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_SMS\_发送\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status)结构。

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


[OID\_WWAN\_SMS\_发送](oid-wwan-sms-send.md)

[**NDIS\_WWAN\_SMS\_发送\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send_status)

 

 




