---
title: OID_WDI_TASK_SEND_REQUEST_ACTION_FRAME
description: OID_WDI_TASK_SEND_REQUEST_ACTION_FRAME 请求的设备操作帧将请求发送到另一台设备。
ms.assetid: CAC86B50-BE85-4650-B6D3-738B4E960587
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_SEND_REQUEST_ACTION_FRAME 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 9871162f5db6f2f44891df01cf87d9f4908bb360
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340081"
---
# <a name="oidwditasksendrequestactionframe"></a>OID\_WDI\_TASK\_SEND\_REQUEST\_ACTION\_FRAME


OID\_WDI\_任务\_发送\_请求\_操作\_帧请求的设备操作帧将请求发送到另一台设备。

| Object | 中止支持                                           | 默认优先级 （主机驱动程序策略） | 正常执行时间 （秒） |
|--------|---------------------------------------------------------|---------------------------------------|---------------------------------|
| 端口   | 是。 端口必须保持干净状态后中止。 | 3                                     | 5                               |

 

此命令是从不同[OID\_WDI\_任务\_发送\_响应\_操作\_帧](oid-wdi-task-send-response-action-frame.md)，这是更多的时间敏感操作。

当设备收到请求帧的确认时，它应在此再次详述同一个通道任务参数中指定 Post ACK 会仔细斟酌次，并应向宿主指示它接收并不会处理本身的任何操作帧。

只要尚未过期的最大超时，设备应重试将公共操作帧发送到远程设备的侦听通道上的远程设备。

任务已完成或者本地设备从远程设备操作帧发送接收确认时，在超时到期，或主机中止操作。 同一个通道停留时间过期后，设备可能表示任务完成。

主机可能会决定中止此操作并继续/重试公共操作帧 exchange，因此，必须在设备是能够快速中止此操作。

## <a name="task-parameters"></a>任务参数


| TLV                                                                                                             | 允许多个 TLV 实例 | 可选 | 描述                                     |
|-----------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------|
| [**WDI\_TLV\_SEND\_ACTION\_FRAME\_REQUEST\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/dn898053) |                                |          | 正在发送操作框架请求参数。 |
| [**WDI\_TLV\_操作\_帧\_正文**](https://msdn.microsoft.com/library/windows/hardware/dn926118)                                         |                                |          | 操作帧正文中。                          |

 

## <a name="task-completion-indication"></a>指示任务完成


[NDIS\_STATUS\_WDI\_INDICATION\_SEND\_REQUEST\_ACTION\_FRAME\_COMPLETE](ndis-status-wdi-indication-send-request-action-frame-complete.md)

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




