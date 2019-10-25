---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION 指示来报告设备服务会话状态更改是由 OID_WWAN_DEVICE_SERVICE_SESSION 生成的。NDIS_WWAN_DEVICE_SERVICE_SESSION_INFO 结构。
ms.assetid: 0A3D8323-20F1-4405-97D4-0E497946118E
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7600f959a03639ea01629c14c4637467a057e122
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843036"
---
# <a name="ndis_status_wwan_device_service_session"></a>\_WWAN\_设备\_SERVICE\_会话的 NDIS\_状态


微型端口驱动程序使用 NDIS\_状态\_WWAN\_设备\_服务\_会话指示报告由[OID\_WWAN\_设备生成的设备服务会话状态更改的完成\_SERVICE\_会话](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-service-session)。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_设备\_服务\_会话\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_info)结构。

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


[OID\_WWAN\_设备\_服务\_会话](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-service-session)

[**NDIS\_WWAN\_设备\_服务\_会话\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_info)

 

 




