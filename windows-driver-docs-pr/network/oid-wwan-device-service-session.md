---
title: OID_WWAN_DEVICE_SERVICE_SESSION
description: OID_WWAN_DEVICE_SERVICE_SESSION 指示微型端口驱动程序打开或关闭设备服务会话。NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION 状态通知，其中包含描述操作结果的 NDIS_WWAN_SET_DEVICE_SERVICE_SESSION 结构。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DEVICE_SERVICE_SESSION 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: aec3d03e92ed5d98f0f24790d9b5c98919b3bd65
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797949"
---
# <a name="oid_wwan_device_service_session"></a>OID \_ WWAN \_ 设备 \_ 服务 \_ 会话


OID \_ WWAN \_ 设备 \_ 服务 \_ 会话定向微型端口驱动程序以打开或关闭设备服务会话。

不支持查询请求。

微型端口驱动程序必须异步处理设置请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，稍后发送 [**ndis \_ 状态 \_ WWAN \_ 设备 \_ 服务 \_ 会话**](./ndis-status-wwan-device-service-session.md) 状态通知，其中包含描述操作结果的 [**ndis \_ WWAN \_ 集 \_ 设备 \_ 服务 \_ 会话**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_set_service_session) 结构。

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


[**NDIS \_ WWAN \_ 设置 \_ 设备 \_ 服务 \_ 会话**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_set_service_session)

[**NDIS \_ 状态 \_ WWAN \_ 设备 \_ 服务 \_ 会话**](./ndis-status-wwan-device-service-session.md)

 

