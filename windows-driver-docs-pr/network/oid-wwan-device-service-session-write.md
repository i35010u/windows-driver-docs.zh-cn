---
title: OID_WWAN_DEVICE_SERVICE_SESSION_WRITE
description: OID_WWAN_DEVICE_SERVICE_SESSION_WRITE 指示微型端口驱动程序将数据写入到 MB 设备，以获取设备服务会话。包含描述操作完成状态的 NDIS_WWAN_DEVICE_SERVICE_SESSION_WRITE_COMPLETE 结构的 NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION_WRITE_COMPLETE 状态通知。
ms.assetid: C1389D7D-3C8E-41B5-8E00-617D699699A2
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DEVICE_SERVICE_SESSION_WRITE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2c27711b22bab463e0262f795b82a6a431a3fec6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843856"
---
# <a name="oid_wwan_device_service_session_write"></a>OID\_WWAN\_设备\_服务\_会话\_写入


OID\_WWAN\_设备\_服务\_会话\_写入指示微型端口驱动程序将数据写入到 MB 设备，以获取设备服务会话。

不支持查询请求。

微型端口驱动程序必须异步处理设置请求，最初返回 NDIS\_状态\_指示\_需要原始请求，稍后将[**ndis\_状态\_WWAN\_设备发送\_服务\_会话\_写入\_完整**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-session-write-complete)状态通知，其中包含[**NDIS\_WWAN\_设备\_SERVICE\_会话\_写入\_完整**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_write_complete)结构，该结构描述操作的完成状态。

如果设备服务会话未打开，微型端口驱动程序应返回 NDIS\_状态\_适配器\_不\_打开。

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


[**NDIS\_状态\_WWAN\_设备\_服务\_会话\_写入\_完成**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-session-write-complete)

[**NDIS\_WWAN\_设备\_服务\_会话\_写入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_session_write)

 

 




