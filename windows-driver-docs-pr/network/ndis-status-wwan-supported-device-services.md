---
title: NDIS_STATUS_WWAN_SUPPORTED_DEVICE_SERVICES
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SUPPORTED_DEVICE_SERVICES 通知来告知 OID_WWAN_ENUMERATE_DEVICE_SERVICES 查询请求的完成 MB 服务。NDIS_WWAN_SUPPORTED_DEVICE_SERVICES 结构。
ms.assetid: 6364DDF7-CE68-4E00-8532-221DD209F145
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_SUPPORTED_DEVICE_SERVICES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6ea6919f395f5e3ee8b3ec88fac237e7d27cedce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372523"
---
# <a name="ndisstatuswwansupporteddeviceservices"></a>NDIS\_状态\_WWAN\_支持\_设备\_服务


微型端口驱动程序使用 NDIS\_状态\_WWAN\_支持\_设备\_服务通知，以关于完成的通知 MB 服务[OID\_WWAN\_ENUMERATE\_设备\_服务](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-enumerate-device-services)查询请求。

微型端口驱动程序不能使用此通知将发送未经请求的事件。

使用此通知[ **NDIS\_WWAN\_支持\_设备\_SERVICES** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_supported_device_services)结构。

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


[OID\_WWAN\_ENUMERATE\_DEVICE\_SERVICES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-enumerate-device-services)

[**NDIS\_WWAN\_SUPPORTED\_DEVICE\_SERVICES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_supported_device_services)

 

 




