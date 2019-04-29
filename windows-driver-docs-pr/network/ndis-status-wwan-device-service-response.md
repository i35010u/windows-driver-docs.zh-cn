---
title: NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE 指示为 OID_WWAN_DEVICE_SERVICE_COMMAND 实现事务完成响应。NDIS_WWAN_DEVICE_SERVICE_RESPONSE 结构。
ms.assetid: 2817EAFA-7A9A-4DC1-B2B7-31E1F4E5E331
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_DEVICE_SERVICE_RESPONSE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4ed8c7044cd8e715203a32c512d4906a1a102dd9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369031"
---
# <a name="ndisstatuswwandeviceserviceresponse"></a>NDIS\_STATUS\_WWAN\_DEVICE\_SERVICE\_RESPONSE


微型端口驱动程序使用 NDIS\_状态\_WWAN\_设备\_服务\_响应指示实现的事务完成响应[OID\_WWAN\_设备\_服务\_命令](https://msdn.microsoft.com/library/windows/hardware/hh440094)。

微型端口驱动程序不能使用此通知将发送未经请求的事件。

使用此通知[ **NDIS\_WWAN\_设备\_服务\_响应**](https://msdn.microsoft.com/library/windows/hardware/hh439838)结构。

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


[OID\_WWAN\_DEVICE\_SERVICE\_COMMAND](https://msdn.microsoft.com/library/windows/hardware/hh440094)

[**NDIS\_WWAN\_DEVICE\_SERVICE\_RESPONSE**](https://msdn.microsoft.com/library/windows/hardware/hh439838)

 

 




