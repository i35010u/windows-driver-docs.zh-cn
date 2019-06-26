---
title: OID_WWAN_DEVICE_SERVICE_SESSION
description: OID_WWAN_DEVICE_SERVICE_SESSION 指示微型端口驱动程序打开或关闭设备服务会话。包含描述操作的结果的 NDIS_WWAN_SET_DEVICE_SERVICE_SESSION 结构 NDIS_STATUS_WWAN_DEVICE_SERVICE_SESSION 状态通知。
ms.assetid: 32D4EDE3-4782-4C54-95B8-83DE7E63C4F8
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DEVICE_SERVICE_SESSION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a6f7880d4ad623390fb39fa4194488b17155d72f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358606"
---
# <a name="oidwwandeviceservicesession"></a>OID\_WWAN\_DEVICE\_SERVICE\_SESSION


OID\_WWAN\_设备\_服务\_会话将定向微型端口驱动程序打开或关闭设备服务会话。

不支持查询请求。

微型端口驱动程序必须处理集请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_设备\_服务\_会话**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-session)状态通知包含[ **NDIS\_WWAN\_设置\_设备\_服务\_会话**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_set_service_session)结构描述操作的结果。

微型端口驱动程序应返回 NDIS\_状态\_不\_如果它们不支持指定的设备服务或操作支持。

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
<td><p>版本：支持 Windows 8 和更高版本的 Windows 中。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_WWAN\_SET\_DEVICE\_SERVICE\_SESSION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_set_service_session)

[**NDIS\_状态\_WWAN\_设备\_服务\_会话**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-session)

 

 




