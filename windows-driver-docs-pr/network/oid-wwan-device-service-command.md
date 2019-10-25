---
title: OID_WWAN_DEVICE_SERVICE_COMMAND
description: OID_WWAN_DEVICE_SERVICE_COMMAND 允许微型端口驱动程序实现特定于供应商的命令。包含供应商定义的结构（NDIS_WWAN_DEVICE_SERVICE_COMMAND）的 NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE 状态通知，用于在完成该事务时提供响应。
ms.assetid: 296E2D23-6EDA-4480-91A3-B6CB39243DAD
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DEVICE_SERVICE_COMMAND 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a046905f185a5d8a0b736997b15fbe9fb1f21493
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843858"
---
# <a name="oid_wwan_device_service_command"></a>OID\_WWAN\_设备\_服务\_命令


OID\_WWAN\_DEVICE\_SERVICE\_命令允许微型端口驱动程序实现特定于供应商的命令。

支持查询和设置请求。

微型端口驱动程序必须异步处理查询和设置请求，最初返回 NDIS\_状态\_指示\_需要请求原始请求，稍后将[**ndis\_状态\_WWAN\_设备发送\_服务\_响应**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-response)状态通知，其中包含供应商定义的结构（[**NDIS\_WWAN\_设备\_SERVICE\_命令**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_command)），以便在用户完成事务时提供响应。

如果不支持指定的设备服务或操作，微型端口驱动程序应返回 NDIS\_状态\_不\_支持。

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


[ **\_WWAN\_设备\_服务\_响应的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-response)

[**NDIS\_WWAN\_设备\_服务\_命令**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_command)

 

 




