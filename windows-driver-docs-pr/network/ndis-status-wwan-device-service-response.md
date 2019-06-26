---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE 指示为 OID_WWAN_DEVICE_SERVICE_COMMAND 实现事务完成响应。NDIS_WWAN_DEVICE_SERVICE_RESPONSE 结构。
ms.assetid: 2817EAFA-7A9A-4DC1-B2B7-31E1F4E5E331
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: dab0f6c21b96673cd6b928e44eb17eba20c1007e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385510"
---
# <a name="ndisstatuswwandeviceserviceresponse"></a>NDIS\_STATUS\_WWAN\_DEVICE\_SERVICE\_RESPONSE


微型端口驱动程序使用 NDIS\_状态\_WWAN\_设备\_服务\_响应指示实现的事务完成响应[OID\_WWAN\_设备\_服务\_命令](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-service-command)。

微型端口驱动程序不能使用此通知将发送未经请求的事件。

使用此通知[ **NDIS\_WWAN\_设备\_服务\_响应**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_response)结构。

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


[OID\_WWAN\_DEVICE\_SERVICE\_COMMAND](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-service-command)

[**NDIS\_WWAN\_DEVICE\_SERVICE\_RESPONSE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_response)

 

 




