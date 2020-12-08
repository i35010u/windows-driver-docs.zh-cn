---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 通知报告 OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS 的查询的完成。NDIS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 结构。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 87504f39f2eab341b7a017808d531302dfcc0497
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803673"
---
# <a name="ndis_status_wwan_device_service_supported_commands"></a>NDIS \_ 状态 \_ WWAN \_ 设备 \_ 服务 \_ 支持的 \_ 命令


微型端口驱动程序使用 NDIS \_ 状态 \_ wwan \_ 设备 \_ 服务支持的 \_ \_ 命令通知报告 [OID \_ WWAN \_ 枚举 \_ 设备 \_ 服务 \_ 命令](./oid-wwan-enumerate-device-service-commands.md)的完成。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用 [**NDIS \_ WWAN \_ 设备 \_ 服务支持的 \_ \_ 命令**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_supported_commands) 结构。

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


[OID \_ WWAN \_ 枚举 \_ 设备 \_ 服务 \_ 命令](./oid-wwan-enumerate-device-service-commands.md)

[**NDIS \_ WWAN \_ 设备 \_ 服务 \_ 支持的 \_ 命令**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_supported_commands)

 

