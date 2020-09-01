---
title: OID_WWAN_DEVICE_SERVICE_SESSION_WRITE
description: OID_WWAN_DEVICE_SERVICE_SESSION_WRITE 指示微型端口驱动程序将数据写入到 MB 设备，以获取设备服务会话。NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION_WRITE_COMPLETE 状态通知，其中包含描述操作完成状态的 NDIS_WWAN_DEVICE_SERVICE_SESSION_WRITE_COMPLETE 结构。
ms.assetid: C1389D7D-3C8E-41B5-8E00-617D699699A2
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DEVICE_SERVICE_SESSION_WRITE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8c4b2767269afc56e9442e9fd69429440554f9f0
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89205979"
---
# <a name="oid_wwan_device_service_session_write"></a>OID \_ WWAN \_ 设备 \_ 服务 \_ 会话 \_ 写入


OID \_ WWAN \_ 设备 \_ 服务 \_ 会话 \_ 写入指示微型端口驱动程序将数据写入到 MB 设备以获取设备服务会话。

不支持查询请求。

微型端口驱动程序必须异步处理设置请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，稍后发送 [**ndis \_ 状态 \_ WWAN \_ 设备 \_ 服务 \_ 会话 \_ 写入 \_ 完整**](./ndis-status-wwan-device-service-session-write-complete.md) 状态通知，其中包含描述操作完成状态的 [**ndis \_ WWAN 设备服务 \_ \_ \_ 会话 \_ \_ **](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_write_complete) 写入完整的状态通知。

\_ \_ \_ 如果未打开设备服务会话，微型端口驱动程序应返回 NDIS 状态适配器 "未 \_ 打开"。

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


[**NDIS \_ 状态 \_ WWAN \_ 设备 \_ 服务 \_ 会话 \_ 写入 \_ 完成**](./ndis-status-wwan-device-service-session-write-complete.md)

[**NDIS \_ WWAN \_ 设备 \_ 服务 \_ 会话 \_ 写入**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_write)

 

