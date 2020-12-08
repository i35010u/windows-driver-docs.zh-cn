---
title: OID_WWAN_DEVICE_SERVICE_COMMAND
description: OID_WWAN_DEVICE_SERVICE_COMMAND 允许微型端口驱动程序实现特定于供应商的命令。包含供应商定义的结构的 NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE 状态通知 (NDIS_WWAN_DEVICE_SERVICE_COMMAND) 在完成该事务时提供响应。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DEVICE_SERVICE_COMMAND 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2b9c400555b78196851998426e20d6cc3b50e0a0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797947"
---
# <a name="oid_wwan_device_service_command"></a>OID \_ WWAN \_ 设备 \_ 服务 \_ 命令


OID \_ WWAN \_ 设备 \_ 服务 \_ 命令允许微型端口驱动程序实现特定于供应商的命令。

支持查询和设置请求。

微型端口驱动程序必须异步处理查询和设置请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，稍后发送 [**ndis \_ 状态 \_ WWAN \_ 设备 \_ 服务 \_ 响应**](./ndis-status-wwan-device-service-response.md) 状态通知，其中包含供应商定义的结构 ([**NDIS \_ WWAN \_ 设备 \_ 服务 \_ 命令**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_command)) 在完成事务后提供响应。

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

## <a name="see-also"></a>请参阅


[**NDIS \_ 状态 \_ WWAN \_ 设备 \_ 服务 \_ 响应**](./ndis-status-wwan-device-service-response.md)

[**NDIS \_ WWAN \_ 设备 \_ 服务 \_ 命令**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_command)

 

