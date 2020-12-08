---
title: NDIS_STATUS_WWAN_SUPPORTED_DEVICE_SERVICES
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SUPPORTED_DEVICE_SERVICES 通知来通知 MB 服务完成 OID_WWAN_ENUMERATE_DEVICE_SERVICES 查询请求。NDIS_WWAN_SUPPORTED_DEVICE_SERVICES 结构。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_SUPPORTED_DEVICE_SERVICES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 966652b2b4cd0862101c9d1988dcde4b8e3fd107
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837115"
---
# <a name="ndis_status_wwan_supported_device_services"></a>NDIS \_ 状态 \_ WWAN \_ 支持的 \_ 设备 \_ 服务


微型端口驱动程序使用 NDIS \_ 状态 \_ wwan 支持的 \_ \_ 设备 \_ 服务通知来通知 MB 服务完成 [OID \_ WWAN \_ 枚举 \_ 设备 \_ 服务](./oid-wwan-enumerate-device-services.md) 查询请求。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用 [**NDIS \_ WWAN 支持 \_ 的 \_ 设备 \_ 服务**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_supported_device_services) 结构。

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

## <a name="see-also"></a>请参阅


[OID \_ WWAN \_ 枚举 \_ 设备 \_ 服务](./oid-wwan-enumerate-device-services.md)

[**NDIS \_ WWAN \_ 支持的 \_ 设备 \_ 服务**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_supported_device_services)

 

