---
title: OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS
description: OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS 返回设备服务支持的命令的列表。NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 状态通知，其中包含描述操作结果的 NDIS_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS 结构。
ms.assetid: 9888E4EC-D4BB-4BAC-B20B-DFA51005EEDA
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a47b2cda830bc2393eebc17c7fcfbd6eeb3ac566
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89205969"
---
# <a name="oid_wwan_enumerate_device_service_commands"></a>OID \_ WWAN \_ 枚举 \_ 设备 \_ 服务 \_ 命令


OID \_ WWAN \_ 枚举 \_ 设备 \_ 服务 \_ 命令返回设备服务支持的命令的列表。

不支持设置请求。

微型端口驱动程序必须异步处理查询请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，稍后发送 [**ndis \_ 状态 \_ WWAN \_ 设备 \_ 服务 \_ 支持的 \_ 命令**](./ndis-status-wwan-device-service-supported-commands.md) 状态通知，其中包含描述操作结果的 [**ndis \_ WWAN \_ 枚举 \_ 设备 \_ 服务 \_ 命令**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_enumerate_device_service_commands) 结构。

如果微型端口驱动程序 \_ 不 \_ \_ 支持指定的设备服务或操作，则它应返回不受支持的 NDIS 状态。

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


[**NDIS \_ 状态 \_ WWAN \_ 设备 \_ 服务 \_ 支持的 \_ 命令**](./ndis-status-wwan-device-service-supported-commands.md)

[**NDIS \_ WWAN \_ 枚举 \_ 设备 \_ 服务 \_ 命令**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_enumerate_device_service_commands)

 

