---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION_READ
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION_READ 通知来通知 MB 服务数据已从打开的设备服务会话中接收。NDIS_WWAN_DEVICE_SERVICE_SESSION_READ 结构。
ms.assetid: 680C15DA-B37C-4A7C-B7BE-B13B3B050EC3
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION_READ 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e7367ea39d88d8340dfb54775cad6a2de39bd50c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838889"
---
# <a name="ndis_status_wwan_device_service_session_read"></a>\_WWAN\_设备\_SERVICE\_会话\_读取的 NDIS\_状态


微型端口驱动程序使用 NDIS\_状态\_WWAN\_设备\_SERVICE\_会话\_读取通知来通知 MB 服务数据已从打开的设备服务会话中接收。

微型端口驱动程序只能使用此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_设备\_服务\_会话\_READ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_read) structure。

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


[**NDIS\_WWAN\_设备\_服务\_会话\_读取**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_read)

 

 




