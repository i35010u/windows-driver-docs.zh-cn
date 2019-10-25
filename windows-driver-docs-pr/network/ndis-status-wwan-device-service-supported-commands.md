---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 通知报告 OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS 查询的完成。NDIS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 结构。
ms.assetid: 3EFEFB4B-6B13-44D7-8788-140B90103A93
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f4af6c66ea19541b61da16a89869f840eef98cc2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843032"
---
# <a name="ndis_status_wwan_device_service_supported_commands"></a>NDIS\_状态\_WWAN\_设备\_服务\_支持的\_命令


微型端口驱动程序使用 NDIS\_状态\_WWAN\_设备\_服务\_支持的\_命令通知，以报告对[OID\_WWAN\_枚举\_设备的查询的完成\_SERVICE\_命令](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-enumerate-device-service-commands)。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_设备\_服务\_支持的\_命令**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_supported_commands)结构。

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


[OID\_WWAN\_枚举\_设备\_服务\_命令](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-enumerate-device-service-commands)

[**NDIS\_WWAN\_设备\_服务\_支持的\_命令**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_service_supported_commands)

 

 




