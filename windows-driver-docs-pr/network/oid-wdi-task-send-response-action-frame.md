---
title: OID_WDI_TASK_SEND_RESPONSE_ACTION_FRAME
description: OID_WDI_TASK_SEND_RESPONSE_ACTION_FRAME IHV 组件发送响应操作帧的请求。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_SEND_RESPONSE_ACTION_FRAME 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 34d5f5a2c750edcea06e777db3e3c6bc3aa6d04c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808045"
---
# <a name="oid_wdi_task_send_response_action_frame"></a>OID \_ WDI \_ TASK \_ 发送 \_ 响应 \_ 操作 \_ 帧


OID \_ WDI \_ TASK \_ 发送 \_ 响应 \_ 操作 \_ 帧请求 IHV 组件发送响应操作帧。

| 对象 | 支持中止                                           | 主机驱动程序策略 (默认优先级)  | 正常执行时间 (秒)  |
|--------|---------------------------------------------------------|---------------------------------------|---------------------------------|
| 端口   | 是的。 中止后，端口必须处于干净状态。 | 3                                     | 5                               |

 

此任务区分时间，必须在收到此数据包的100毫秒内提供服务。

当最大超时未过期时，端口应重试将帧发送到指定通道上的远程设备。

当本地设备接收到发送的操作帧的确认、超时过期或主机中止操作时，任务完成。 在同一通道停留时间到期后，设备可能会指示任务完成。

主机可能决定中止此操作并继续/重试操作帧交换，因此设备必须能够快速中止此操作。

## <a name="task-parameters"></a>任务参数


| TLV                                                                                                               | 允许多个 TLV 实例 | 可选 | 说明                                      |
|-------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------|
| [**WDI \_ TLV \_ 发送 \_ 操作 \_ 帧 \_ 响应 \_ 参数**](./wdi-tlv-send-action-frame-response-parameters.md) |                                |          | 用于发送操作帧响应的参数。 |
| [**WDI \_ TLV \_ 操作 \_ 框架 \_ 正文**](./wdi-tlv-action-frame-body.md)                                           |                                |          | 操作框架正文。                           |

 

## <a name="task-completion-indication"></a>任务完成指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ 发送 \_ 响应 \_ 操作 \_ 帧 \_ 完成](ndis-status-wdi-indication-send-response-action-frame-complete.md)

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

