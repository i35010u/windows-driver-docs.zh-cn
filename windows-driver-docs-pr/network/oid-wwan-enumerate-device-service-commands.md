---
title: OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS
description: OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS 返回设备服务支持的命令的列表。NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 状态通知，其中包含描述操作结果的 NDIS_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS 结构。
ms.assetid: 9888E4EC-D4BB-4BAC-B20B-DFA51005EEDA
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a0122e4de6641c99a265d6c3e82d2a5980e0b76e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843845"
---
# <a name="oid_wwan_enumerate_device_service_commands"></a>OID\_WWAN\_枚举\_设备\_服务\_命令


OID\_WWAN\_枚举\_设备\_服务\_命令返回设备服务支持的命令列表。

不支持设置请求。

微型端口驱动程序必须异步处理查询请求，最初返回 NDIS\_状态\_指示\_需要请求原始请求，稍后将[**ndis\_状态\_WWAN\_设备发送\_服务\_支持\_命令**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands)状态通知，其中包含[**NDIS\_WWAN\_枚举\_设备\_SERVICE\_命令**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_enumerate_device_service_commands)结构，用于描述操作的结果。

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


[**NDIS\_状态\_WWAN\_设备\_服务\_支持的\_命令**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-service-supported-commands)

[**NDIS\_WWAN\_枚举\_设备\_服务\_命令**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_enumerate_device_service_commands)

 

 




