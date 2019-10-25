---
title: OID_WWAN_DEVICE_SERVICE_SESSION
description: OID_WWAN_DEVICE_SERVICE_SESSION 指示微型端口驱动程序打开或关闭设备服务会话。NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION 状态通知，其中包含描述操作结果的 NDIS_WWAN_SET_DEVICE_SERVICE_SESSION 结构。
ms.assetid: 32D4EDE3-4782-4C54-95B8-83DE7E63C4F8
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DEVICE_SERVICE_SESSION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c14bb312773365fc1000a1edf5c6a2f404261277
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843852"
---
# <a name="oid_wwan_device_service_session"></a>OID\_WWAN\_设备\_服务\_会话


OID\_WWAN\_设备\_服务\_会话定向微型端口驱动程序以打开或关闭设备服务会话。

不支持查询请求。

微型端口驱动程序必须异步处理设置请求，最初返回 NDIS\_状态\_指示\_需要原始请求，稍后将[**ndis\_状态\_WWAN\_设备发送\_服务\_会话**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-session)状态通知，其中包含一个[**NDIS\_WWAN\_集\_设备\_服务\_会话**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_set_service_session)结构，该结构描述操作的结果。

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


[**NDIS\_WWAN\_集\_设备\_服务\_会话**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_set_service_session)

[ **\_WWAN\_设备\_SERVICE\_会话的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-session)

 

 




