---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 通知来报告已完成的 OID_WWAN_ENUMERATE_DEVICE_SERVICE_COMMANDS 查询。NDIS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 结构。
ms.assetid: 3EFEFB4B-6B13-44D7-8788-140B90103A93
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_DEVICE_SERVICE_SUPPORTED_COMMANDS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b6f9d6f5b41c30704d9ed3f4d3f92e46287e1468
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343283"
---
# <a name="ndisstatuswwandeviceservicesupportedcommands"></a>NDIS\_状态\_WWAN\_设备\_服务\_支持\_命令


微型端口驱动程序使用 NDIS\_状态\_WWAN\_设备\_服务\_支持\_报告已完成的查询命令通知[OID\_WWAN\_ENUMERATE\_设备\_服务\_命令](https://msdn.microsoft.com/library/windows/hardware/hh846221)。

微型端口驱动程序不能使用此通知将发送未经请求的事件。

使用此通知[ **NDIS\_WWAN\_设备\_服务\_支持\_命令**](https://msdn.microsoft.com/library/windows/hardware/hh846214)结构。

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


[OID\_WWAN\_ENUMERATE\_DEVICE\_SERVICE\_COMMANDS](https://msdn.microsoft.com/library/windows/hardware/hh846221)

[**NDIS\_WWAN\_DEVICE\_SERVICE\_SUPPORTED\_COMMANDS**](https://msdn.microsoft.com/library/windows/hardware/hh846214)

 

 




