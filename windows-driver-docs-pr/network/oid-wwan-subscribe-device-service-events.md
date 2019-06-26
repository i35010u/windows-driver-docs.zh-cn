---
title: OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS
description: OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS 设置有关列表的 MB 设备必须发送 NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT 通知的设备服务的信息。
ms.assetid: 34D38A28-0E81-47B0-9232-F89927DA4B2B
ms.date: 08/08/2017
keywords: -OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a11d2326aa9cc9c17365dff64642485787f9edff
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384718"
---
# <a name="oidwwansubscribedeviceserviceevents"></a>OID\_WWAN\_SUBSCRIBE\_设备\_服务\_事件


OID\_WWAN\_SUBSCRIBE\_设备\_服务\_事件集的列表信息的设备服务的 MB 设备必须发送[ **NDIS\_状态\_WWAN\_设备\_服务\_事件**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event)通知。 MB 设备应指示任何设备服务不在此列表中的事件。

微型端口驱动程序必须处理集请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_设备\_服务\_订阅**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription)包含的 MB 设备上的事件订阅的当前列表的状态通知。

调用方请求设置的 MB 设备服务事件订阅列表提供[ **NDIS\_WWAN\_SUBSCRIBE\_设备\_服务\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_subscribe_device_service_events)微型端口驱动程序的相应信息的结构。

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
<td><p>版本：支持 Windows 8 和更高版本的 Windows 中。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_STATUS\_WWAN\_DEVICE\_SERVICE\_EVENT**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event)

[**NDIS\_状态\_WWAN\_设备\_服务\_订阅**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription)

[**NDIS\_WWAN\_SUBSCRIBE\_设备\_服务\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_subscribe_device_service_events)

 

 




