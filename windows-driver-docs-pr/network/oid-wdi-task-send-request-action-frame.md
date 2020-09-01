---
title: OID_WDI_TASK_SEND_REQUEST_ACTION_FRAME
description: OID_WDI_TASK_SEND_REQUEST_ACTION_FRAME 请求设备将操作帧请求发送到另一台设备。
ms.assetid: CAC86B50-BE85-4650-B6D3-738B4E960587
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_SEND_REQUEST_ACTION_FRAME 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: ccdf9aa027ecbd16a7981d6d3b719ef5cdca9470
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217247"
---
# <a name="oid_wdi_task_send_request_action_frame"></a>OID \_ WDI \_ TASK \_ 发送 \_ 请求 \_ 操作 \_ 框架


OID \_ WDI \_ TASK \_ 发送 \_ 请求 \_ 操作 \_ 帧请求设备向另一台设备发送操作帧请求。

| 对象 | 支持中止                                           | 主机驱动程序策略 (默认优先级)  | 正常执行时间 (秒)  |
|--------|---------------------------------------------------------|---------------------------------------|---------------------------------|
| 端口   | 是。 中止后，端口必须处于干净状态。 | 3                                     | 5                               |

 

此命令不同于 [OID \_ WDI \_ TASK \_ 发送 \_ 响应 \_ 操作 \_ 框架](oid-wdi-task-send-response-action-frame.md)，这是一项比较时间敏感的操作。

当设备接收到请求帧的确认时，它应停留在任务参数中指定的 ACK 停留时间的相同通道上，并向宿主指示它接收的任何操作帧，而不会自行处理。

只要最大超时未过期，设备应重试将公共操作帧发送到远程设备的侦听通道上的远程设备。

当本地设备接收到发送的操作帧的确认、超时过期或主机中止操作时，任务完成。 在同一通道停留时间到期后，设备可能会指示任务完成。

主机可能决定中止此操作并继续/重试公共操作帧交换，因此设备必须能够快速中止此操作。

## <a name="task-parameters"></a>任务参数


| TLV                                                                                                             | 允许多个 TLV 实例 | 可选 | 说明                                     |
|-----------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------|
| [**WDI \_ TLV \_ 发送 \_ 操作 \_ 帧 \_ 请求 \_ 参数**](./wdi-tlv-send-action-frame-request-parameters.md) |                                |          | 用于发送操作帧请求的参数。 |
| [**WDI \_ TLV \_ 操作 \_ 框架 \_ 正文**](./wdi-tlv-action-frame-body.md)                                         |                                |          | 操作框架正文。                          |

 

## <a name="task-completion-indication"></a>任务完成指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ 发送 \_ 请求 \_ 操作 \_ 帧 \_ 完成](ndis-status-wdi-indication-send-request-action-frame-complete.md)

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
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

