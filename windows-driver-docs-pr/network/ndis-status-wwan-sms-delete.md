---
title: NDIS_STATUS_WWAN_SMS_DELETE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SMS_DELETE 通知来通知关于完成的上一个 delete 请求通过 OID_WWAN_SMS_DELETE MB 服务。
ms.assetid: 0083dcd9-4e18-4582-993a-c4402cb552de
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SMS_DELETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7bead5976d32c229c9527615f0395d25fe9a5bee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541822"
---
# <a name="ndisstatuswwansmsdelete"></a>NDIS\_状态\_WWAN\_SMS\_删除


微型端口驱动程序使用 NDIS\_状态\_WWAN\_SMS\_删除通知来通知关于完成的上一个 delete 请求通过 MB 服务[OID\_WWAN\_短信\_删除](oid-wwan-sms-delete.md)。

微型端口驱动程序不能使用此通知将发送未经请求的事件。

使用此通知[ **NDIS\_WWAN\_SMS\_删除\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567940)结构。

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
<td><p>标头</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_WWAN\_SMS\_DELETE](oid-wwan-sms-delete.md)

[**NDIS\_WWAN\_SMS\_删除\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567940)

 

 




