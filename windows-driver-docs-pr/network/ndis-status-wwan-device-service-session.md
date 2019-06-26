---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION 指示报告由 OID_WWAN_DEVICE_SERVICE_SESSION 产生设备服务会话状态更改的完成。NDIS_WWAN_DEVICE_SERVICE_SESSION_INFO 结构。
ms.assetid: 0A3D8323-20F1-4405-97D4-0E497946118E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9d72398ef20047bb1afd4ffafcb63445fb0d2f2e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366607"
---
# <a name="ndisstatuswwandeviceservicesession"></a>NDIS\_状态\_WWAN\_设备\_服务\_会话


微型端口驱动程序使用 NDIS\_状态\_WWAN\_设备\_服务\_由发起会话表示要报告的设备服务会话状态更改完成[OID\_WWAN\_设备\_服务\_会话](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-service-session)。

微型端口驱动程序不能使用此通知将发送未经请求的事件。

使用此通知[ **NDIS\_WWAN\_设备\_服务\_会话\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_info)结构。

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


[OID\_WWAN\_DEVICE\_SERVICE\_SESSION](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-service-session)

[**NDIS\_WWAN\_DEVICE\_SERVICE\_SESSION\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_info)

 

 




