---
title: NDIS_STATUS_WWAN_DEVICE_CAPS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_CAPS 通知来响应 OID_WWAN_DEVICE_CAPS 查询请求。 微型端口驱动程序不能使用此通知将发送未经请求的事件。此通知使用 NDIS_WWAN_DEVICE_CAPS 结构。
ms.assetid: e21e2928-c50d-4dec-a575-7e306fecf20f
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_DEVICE_CAPS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7db36d959fb538fcbb35a5c49f11b7519e47fb2c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523526"
---
# <a name="ndisstatuswwandevicecaps"></a>NDIS\_STATUS\_WWAN\_DEVICE\_CAPS


微型端口驱动程序使用 NDIS\_状态\_WWAN\_设备\_CAPS 通知以响应[OID\_WWAN\_设备\_CAPS](https://msdn.microsoft.com/library/windows/hardware/ff569824)查询请求。

微型端口驱动程序不能使用此通知将发送未经请求的事件。

使用此通知[ **NDIS\_WWAN\_设备\_CAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff567907)结构。

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


[OID\_WWAN\_DEVICE\_CAPS](https://msdn.microsoft.com/library/windows/hardware/ff569824)

[**NDIS\_WWAN\_DEVICE\_CAPS**](https://msdn.microsoft.com/library/windows/hardware/ff567907)

 

 




