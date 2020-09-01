---
title: OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS
description: OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS 设置有关设备服务列表的信息，MB 设备必须将其发送 NDIS_STATUS_WWAN_DEVICE_SERVICE_EVENT 通知。
ms.assetid: 34D38A28-0E81-47B0-9232-F89927DA4B2B
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 99dc40288f5cd3cd652a31fde7881376180fd654
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211647"
---
# <a name="oid_wwan_subscribe_device_service_events"></a>OID \_ WWAN \_ 订阅 \_ 设备 \_ 服务 \_ 事件


OID \_ WWAN \_ 订阅 \_ 设备 \_ 服务 \_ 事件设置设备服务列表的相关信息，MB 设备必须发送 [**NDIS \_ 状态 \_ WWAN \_ 设备 \_ 服务 \_ 事件**](./ndis-status-wwan-device-service-event.md) 通知。 MB 设备不应为不在此列表中的任何设备服务指示事件。

微型端口驱动程序必须异步处理设置请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，稍后发送 [**NDIS \_ 状态 \_ WWAN \_ 设备 \_ 服务 \_ 订阅**](./ndis-status-wwan-device-service-subscription.md) 状态通知，其中包含 MB 设备上的当前事件订阅列表。

请求设置 MB 设备服务事件订阅列表的调用方使用合适的信息为微型端口驱动程序提供 [**NDIS \_ WWAN \_ 订阅 \_ 设备 \_ 服务 \_ 事件**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_subscribe_device_service_events) 结构。

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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ 状态 \_ WWAN \_ 设备 \_ 服务 \_ 事件**](./ndis-status-wwan-device-service-event.md)

[**NDIS \_ 状态 \_ WWAN \_ 设备 \_ 服务 \_ 订阅**](./ndis-status-wwan-device-service-subscription.md)

[**NDIS \_ WWAN \_ 订阅 \_ 设备 \_ 服务 \_ 事件**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_subscribe_device_service_events)

 

