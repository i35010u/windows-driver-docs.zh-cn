---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION
description: 小型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION 通知来通知 MB 服务有关设备服务的订阅，以响应 OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS 的请求。NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION 结构。
ms.assetid: E2B839AE-F81A-41EE-8374-F830B79D1E74
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7e427fd822159dcb0e61a6cbedfdc07b4c3af03b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212857"
---
# <a name="ndis_status_wwan_device_service_subscription"></a>NDIS \_ 状态 \_ WWAN \_ 设备 \_ 服务 \_ 订阅


微型端口驱动程序使用 NDIS \_ 状态 \_ WWAN \_ 设备 \_ 服务 \_ 订阅通知来通知 MB 服务设备服务订阅，以响应 [OID \_ WWAN \_ 订阅 \_ 设备 \_ 服务 \_ 事件](./oid-wwan-subscribe-device-service-events.md) 集请求。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此指示使用 [**NDIS \_ WWAN \_ 设备 \_ 服务 \_ 订阅**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_subscription) 结构。

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


[OID \_ WWAN \_ 订阅 \_ 设备 \_ 服务 \_ 事件](./oid-wwan-subscribe-device-service-events.md)

[**NDIS \_ WWAN \_ 设备 \_ 服务 \_ 订阅**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_subscription)

 

