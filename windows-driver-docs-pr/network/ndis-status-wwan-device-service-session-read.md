---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION_READ
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION_READ 通知来告知 MB 服务已从打开的设备服务会话收到数据。NDIS_WWAN_DEVICE_SERVICE_SESSION_READ 结构。
ms.assetid: 680C15DA-B37C-4A7C-B7BE-B13B3B050EC3
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION_READ 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 037d00c44b3a6f0973c6182165ac1afcf619dfe1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366611"
---
# <a name="ndisstatuswwandeviceservicesessionread"></a>NDIS\_STATUS\_WWAN\_DEVICE\_SERVICE\_SESSION\_READ


微型端口驱动程序使用 NDIS\_状态\_WWAN\_设备\_服务\_会话\_读取通知来通知 MB 服务从打开的设备服务接收到数据会话。

微型端口驱动程序只能使用此通知将发送未经请求的事件。

使用此通知[ **NDIS\_WWAN\_设备\_服务\_会话\_读取**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_read)结构。

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
<td><p>支持从 Windows 8 开始。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_WWAN\_DEVICE\_SERVICE\_SESSION\_READ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_read)

 

 




