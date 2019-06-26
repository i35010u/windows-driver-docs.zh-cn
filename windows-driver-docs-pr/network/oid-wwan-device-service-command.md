---
title: OID_WWAN_DEVICE_SERVICE_COMMAND
description: OID_WWAN_DEVICE_SERVICE_COMMAND 允许微型端口驱动程序来实现供应商特定的命令。NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE 状态通知，其中包含供应商定义的结构 (NDIS_WWAN_DEVICE_SERVICE_COMMAND) 当他们已完成事务时提供响应。
ms.assetid: 296E2D23-6EDA-4480-91A3-B6CB39243DAD
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DEVICE_SERVICE_COMMAND 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7f81f9873ecbfbc7896e101aac82d94560981281
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362836"
---
# <a name="oidwwandeviceservicecommand"></a>OID\_WWAN\_设备\_服务\_命令


OID\_WWAN\_设备\_服务\_命令允许微型端口驱动程序来实现供应商特定的命令。

两种查询和支持集请求。

微型端口驱动程序必须处理查询并集请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_设备\_服务\_响应**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-response)包含供应商定义的结构的状态通知 ([**NDIS\_WWAN\_设备\_服务\_命令**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_command)) 当他们已完成事务时提供响应。

微型端口驱动程序应返回 NDIS\_状态\_不\_如果它们不支持指定的设备服务或操作支持。

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


[**NDIS\_状态\_WWAN\_设备\_服务\_响应**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-response)

[**NDIS\_WWAN\_DEVICE\_SERVICE\_COMMAND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_command)

 

 




