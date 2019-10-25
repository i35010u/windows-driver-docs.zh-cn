---
title: OID_WWAN_ENUMERATE_DEVICE_SERVICES
description: OID_WWAN_ENUMERATE_DEVICE_SERVICES 返回微型端口驱动程序所支持的设备服务的列表。NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 状态通知，其中包含提供受支持的设备服务 Guid 列表的 NDIS_WWAN_SUPPORTED_DEVICE_SERVICES 结构。
ms.assetid: 12AB2235-DDF8-44CB-BD3D-61D0FFCB4080
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_ENUMERATE_DEVICE_SERVICES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 47279d09418e78a2359b296a4e2f19ef7a599141
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843844"
---
# <a name="oid_wwan_enumerate_device_services"></a>OID\_WWAN\_枚举\_设备\_服务


OID\_WWAN\_枚举\_设备\_服务返回微型端口驱动程序所支持的设备服务列表。

不支持设置请求。

微型端口驱动程序必须异步处理查询请求，最初返回 NDIS\_状态\_指示\_需要请求原始请求，稍后将[**ndis\_状态\_WWAN\_设备发送\_服务\_支持的\_命令**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands)状态通知，其中包含一个[**NDIS\_WWAN\_支持的\_设备\_SERVICES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_supported_device_services)结构，提供受支持的设备服务 guid 列表。

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


[**NDIS\_状态\_WWAN\_设备\_服务\_支持的\_命令**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands)

[**NDIS\_WWAN\_支持\_设备\_服务**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_supported_device_services)

 

 




