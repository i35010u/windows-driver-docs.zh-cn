---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION 通知来通知 MB 服务有关设备服务的订阅，以响应 OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS 的请求。NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION 结构。
ms.assetid: E2B839AE-F81A-41EE-8374-F830B79D1E74
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 038ddc7e5bbff54eadf84cfc4d0aa4743841782b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843034"
---
# <a name="ndis_status_wwan_device_service_subscription"></a>\_WWAN\_设备\_SERVICE\_订阅的 NDIS\_状态


小型端口驱动程序使用 NDIS\_状态\_WWAN\_设备\_服务\_订阅通知来通知 MB 服务有关设备服务订阅的信息，以响应[OID\_WWAN\_订阅\_设备\_服务\_事件](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-subscribe-device-service-events)设置请求。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此指示使用[**NDIS\_WWAN\_设备\_服务\_订阅**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_subscription)结构。

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
<td><p>从 Windows 8 开始支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_WWAN\_订阅\_设备\_服务\_事件](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-subscribe-device-service-events)

[**NDIS\_WWAN\_设备\_服务\_订阅**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_subscription)

 

 




