---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE 指示来实现 OID_WWAN_DEVICE_SERVICE_COMMAND 的事务完成响应。NDIS_WWAN_DEVICE_SERVICE_RESPONSE 结构。
ms.assetid: 2817EAFA-7A9A-4DC1-B2B7-31E1F4E5E331
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9d04dfbb8de4abf3f31d69e1469e9602b3770e99
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842645"
---
# <a name="ndis_status_wwan_device_service_response"></a>\_WWAN\_设备\_服务\_响应的 NDIS\_状态


小型端口驱动程序使用 NDIS\_状态\_WWAN\_设备\_服务\_响应指示来实现[OID\_WWAN\_设备\_SERVICE\_命令的事务完成响应](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-service-command).

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_设备\_服务\_响应**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_response)结构。

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


[OID\_WWAN\_设备\_服务\_命令](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-service-command)

[**NDIS\_WWAN\_设备\_服务\_响应**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_response)

 

 




