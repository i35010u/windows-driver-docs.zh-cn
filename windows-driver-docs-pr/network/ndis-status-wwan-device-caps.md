---
title: NDIS_STATUS_WWAN_DEVICE_CAPS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_CAPS 通知来响应 OID_WWAN_DEVICE_CAPS 查询请求。 微型端口驱动程序无法使用此通知发送未经请求的事件。此通知使用 NDIS_WWAN_DEVICE_CAPS 结构。
ms.assetid: e21e2928-c50d-4dec-a575-7e306fecf20f
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_CAPS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e98e2ed9a5f3ab6dd2f70caad0380595098ba277
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842633"
---
# <a name="ndis_status_wwan_device_caps"></a>\_WWAN\_设备\_CAP 的 NDIS\_状态


小型端口驱动程序使用 NDIS\_状态\_WWAN\_设备\_CAP 通知，以响应[OID\_wwan\_设备\_cap](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps)查询请求。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_设备\_cap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)结构。

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


[OID\_WWAN\_设备\_CAP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps)

[**NDIS\_WWAN\_设备\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)

 

 




