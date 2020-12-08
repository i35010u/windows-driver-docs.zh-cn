---
title: OID_WWAN_ENUMERATE_DEVICE_SERVICES
description: OID_WWAN_ENUMERATE_DEVICE_SERVICES 返回微型端口驱动程序所支持的设备服务的列表。NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 状态通知，其中包含提供受支持的设备服务 Guid 列表的 NDIS_WWAN_SUPPORTED_DEVICE_SERVICES 结构。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_ENUMERATE_DEVICE_SERVICES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f38a6cbd5e6a8b56489d832c46ca4a74704fce5e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823823"
---
# <a name="oid_wwan_enumerate_device_services"></a>OID \_ WWAN \_ 枚举 \_ 设备 \_ 服务


OID \_ WWAN \_ 枚举 \_ 设备 \_ 服务返回微型端口驱动程序所支持的设备服务列表。

不支持设置请求。

微型端口驱动程序必须异步处理查询请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，稍后发送 [**ndis \_ 状态 \_ WWAN \_ 设备 \_ 服务 \_ 支持的 \_ 命令**](./ndis-status-wwan-device-service-supported-commands.md) 状态通知，其中包含提供支持的设备服务 guid 列表的 [**ndis \_ WWAN 支持的 \_ \_ 设备 \_ 服务**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_supported_device_services) 结构。

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

## <a name="see-also"></a>请参阅


[**NDIS \_ 状态 \_ WWAN \_ 设备 \_ 服务 \_ 支持的 \_ 命令**](./ndis-status-wwan-device-service-supported-commands.md)

[**NDIS \_ WWAN \_ 支持的 \_ 设备 \_ 服务**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_supported_device_services)

 

