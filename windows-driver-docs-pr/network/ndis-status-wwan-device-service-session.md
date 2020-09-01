---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION 指示报告 OID_WWAN_DEVICE_SERVICE_SESSION 的设备服务会话状态更改是否完成。NDIS_WWAN_DEVICE_SERVICE_SESSION_INFO 结构。
ms.assetid: 0A3D8323-20F1-4405-97D4-0E497946118E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4138f7ae733000567869aeec7f4903108e05c7c8
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215502"
---
# <a name="ndis_status_wwan_device_service_session"></a>NDIS \_ 状态 \_ WWAN \_ 设备 \_ 服务 \_ 会话


微型端口驱动程序使用 NDIS \_ 状态 " \_ WWAN \_ 设备 \_ 服务 \_ 会话指示" 报告由 [OID \_ WWAN \_ 设备 \_ 服务 \_ 会话](./oid-wwan-device-service-session.md)生成的设备服务会话状态更改的完成。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用 [**NDIS \_ WWAN \_ 设备 \_ 服务 \_ 会话 \_ 信息**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_info) 结构。

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


[OID \_ WWAN \_ 设备 \_ 服务 \_ 会话](./oid-wwan-device-service-session.md)

[**NDIS \_ WWAN \_ 设备 \_ 服务 \_ 会话 \_ 信息**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_info)

 

