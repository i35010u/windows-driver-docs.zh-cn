---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION 通知来告知 OID_WWAN_SUBSCRIBE_DEVICE_SERVICE_EVENTS 集请求的响应中的设备服务订阅 MB 服务。NDIS_WWAN_DEVICE_SERVICE_SUBSCRIPTION 结构。
ms.assetid: E2B839AE-F81A-41EE-8374-F830B79D1E74
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_DEVICE_SERVICE_SUBSCRIPTION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a11ecfb82123353d3b1b890c6d7bde2560c933de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521302"
---
# <a name="ndisstatuswwandeviceservicesubscription"></a>NDIS\_状态\_WWAN\_设备\_服务\_订阅


微型端口驱动程序使用 NDIS\_状态\_WWAN\_设备\_服务\_订阅通知，以通知 MB 服务响应中的设备服务订阅有关[OID\_WWAN\_SUBSCRIBE\_设备\_服务\_事件](https://msdn.microsoft.com/library/windows/hardware/hh440096)集请求。

微型端口驱动程序不能使用此通知将发送未经请求的事件。

此指示使用[ **NDIS\_WWAN\_设备\_服务\_订阅**](https://msdn.microsoft.com/library/windows/hardware/hh439839)结构。

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
<td><p>支持从 Windows 8 开始。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_WWAN\_SUBSCRIBE\_DEVICE\_SERVICE\_EVENTS](https://msdn.microsoft.com/library/windows/hardware/hh440096)

[**NDIS\_WWAN\_设备\_服务\_订阅**](https://msdn.microsoft.com/library/windows/hardware/hh439839)

 

 




