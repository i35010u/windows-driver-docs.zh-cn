---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION 通知来告知 OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS 集请求的响应中的设备服务订阅 MB 服务。NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION 结构。
ms.assetid: E2B839AE-F81A-41EE-8374-F830B79D1E74
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: efbe036efb411c9649bdecb12166cb967b67453f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366606"
---
# <a name="ndisstatuswwandeviceservicesubscription"></a>NDIS\_状态\_WWAN\_设备\_服务\_订阅


微型端口驱动程序使用 NDIS\_状态\_WWAN\_设备\_服务\_订阅通知，以通知 MB 服务响应中的设备服务订阅有关[OID\_WWAN\_SUBSCRIBE\_设备\_服务\_事件](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-subscribe-device-service-events)集请求。

微型端口驱动程序不能使用此通知将发送未经请求的事件。

此指示使用[ **NDIS\_WWAN\_设备\_服务\_订阅**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_subscription)结构。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>支持从 Windows 8 开始。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID\_WWAN\_SUBSCRIBE\_DEVICE\_SERVICE\_EVENTS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-subscribe-device-service-events)

[**NDIS\_WWAN\_设备\_服务\_订阅**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_subscription)

 

 




