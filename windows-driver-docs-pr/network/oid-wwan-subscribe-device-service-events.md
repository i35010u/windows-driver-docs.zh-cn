---
title: OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS
description: OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS 设置有关设备服务列表的信息，MB 设备必须将其发送 NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT 通知。
ms.assetid: 34D38A28-0E81-47B0-9232-F89927DA4B2B
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 12afb51891a3b42e32b9ab1ccd20deb32261cb9b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843780"
---
# <a name="oid_wwan_subscribe_device_service_events"></a>OID\_WWAN\_订阅\_设备\_服务\_事件


OID\_WWAN\_订阅\_设备\_服务\_事件设置有关设备服务列表的信息，在该设备服务中，MB 设备必须发送[**NDIS\_状态\_WWAN\_设备\_服务\_事件**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event)通知。 MB 设备不应为不在此列表中的任何设备服务指示事件。

微型端口驱动程序必须异步处理设置请求，最初返回 NDIS\_状态\_指示\_需要原始请求，稍后将[**ndis\_状态\_WWAN\_设备发送\_服务\_订阅**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription)状态通知，其中包含 MB 设备上的当前事件订阅列表。

请求设置 MB 设备服务事件订阅列表的调用方提供[**NDIS\_WWAN\_使用适当的信息订阅\_设备\_服务\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_subscribe_device_service_events)结构。

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
<td><p>版本：在 windows 8 及更高版本的 Windows 中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[ **\_WWAN\_设备\_SERVICE\_事件的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-event)

[ **\_WWAN\_设备\_SERVICE\_订阅的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-subscription)

[**NDIS\_WWAN\_订阅\_设备\_服务\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_subscribe_device_service_events)

 

 




