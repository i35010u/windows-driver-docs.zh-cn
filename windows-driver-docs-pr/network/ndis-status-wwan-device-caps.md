---
title: NDIS_STATUS_WWAN_DEVICE_CAPS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_CAPS 通知来响应 OID_WWAN_DEVICE_CAPS 查询请求。 微型端口驱动程序无法使用此通知发送未经请求的事件。此通知使用 NDIS_WWAN_DEVICE_CAPS 结构。
ms.assetid: e21e2928-c50d-4dec-a575-7e306fecf20f
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_DEVICE_CAPS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d969079301efbba5551530e62a09647027dd6caa
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209693"
---
# <a name="ndis_status_wwan_device_caps"></a>NDIS \_ 状态 \_ WWAN \_ 设备 \_ CAP


微型端口驱动程序使用 NDIS \_ 状态 \_ wwan \_ 设备 \_ Cap 通知来响应 [OID \_ WWAN \_ 设备 \_ cap](./oid-wwan-device-caps.md) 查询请求。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用 [**NDIS \_ WWAN \_ 设备 \_ cap**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps) 结构。

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


[OID \_ WWAN \_ 设备 \_ CAP](./oid-wwan-device-caps.md)

[**NDIS \_ WWAN \_ 设备 \_ CAP**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps)

 

