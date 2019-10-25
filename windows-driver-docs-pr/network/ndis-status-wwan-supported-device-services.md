---
title: NDIS_STATUS_WWAN_SUPPORTED_DEVICE_SERVICES
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SUPPORTED_DEVICE_SERVICES 通知来通知 MB 服务完成 OID_WWAN_ENUMERATE_DEVICE_SERVICES 查询请求。NDIS_WWAN_SUPPORTED_DEVICE_SERVICES 结构。
ms.assetid: 6364DDF7-CE68-4E00-8532-221DD209F145
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_SUPPORTED_DEVICE_SERVICES 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7a14441f7334252fe64ab176e3eb4ea030b282d7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844628"
---
# <a name="ndis_status_wwan_supported_device_services"></a>NDIS\_状态\_WWAN\_支持\_设备\_服务


微型端口驱动程序使用 NDIS\_状态\_WWAN\_支持\_设备\_SERVICES 通知来通知 MB 服务完成[OID\_WWAN\_枚举\_设备\_服务](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-enumerate-device-services)查询请求。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_支持\_设备\_SERVICES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_supported_device_services)结构。

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


[OID\_WWAN\_枚举\_设备\_服务](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-enumerate-device-services)

[**NDIS\_WWAN\_支持\_设备\_服务**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_supported_device_services)

 

 




