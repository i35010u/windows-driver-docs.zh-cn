---
title: NDIS_STATUS_WWAN_SMS_DELETE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SMS_DELETE 通知来通知 MB 服务通过 OID_WWAN_SMS_DELETE 完成以前的删除请求。
ms.assetid: 0083dcd9-4e18-4582-993a-c4402cb552de
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SMS_DELETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 996f9b9b4acde47d13f5403f80d1ffd236bed17b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844634"
---
# <a name="ndis_status_wwan_sms_delete"></a>\_WWAN\_SMS\_删除的 NDIS\_状态


微型端口驱动程序使用 NDIS\_状态\_WWAN\_SMS\_删除通知，通过[OID\_wwan\_SMS\_删除](oid-wwan-sms-delete.md)通知 MB 服务，通知 MB 服务已完成以前的 DELETE 请求。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_SMS\_删除\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete_status)结构。

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


[OID\_WWAN\_SMS\_删除](oid-wwan-sms-delete.md)

[**NDIS\_WWAN\_SMS\_删除\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete_status)

 

 




