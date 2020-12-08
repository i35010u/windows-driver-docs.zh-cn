---
title: OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME
description: 将 OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME 颁发给 IHV 组件，以便向对等方发送 Wi-Fi 的直接公共操作帧请求。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: cf84c65735c528d82978c269586951482488864f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829243"
---
# <a name="oid_wdi_task_p2p_send_response_action_frame"></a>OID \_ WDI \_ 任务 \_ P2P \_ 发送 \_ 响应 \_ 操作 \_ 帧


OID \_ WDI \_ 任务 \_ P2P \_ 发送 \_ 响应 \_ 操作 \_ 帧颁发给 IHV 组件，以将 Wi-Fi 直接公共操作帧请求发送到对等方。

| 对象 | 支持中止                                           | 主机驱动程序策略 (默认优先级)  | 正常执行时间 (秒)  |
|--------|---------------------------------------------------------|---------------------------------------|---------------------------------|
| 端口   | 是的。 中止后，端口必须处于干净状态。 | 3                                     | 5                               |

 

当端口收到请求帧的确认时，它应停留在100ms 的同一通道上，并指示它接收到主机的任何 Wi-Fi 直接公共操作帧。

此任务区分时间。 Wi-Fi 直接规范要求发送 Wi-Fi 直接操作响应仅在收到此数据包的100毫秒内提供。

由于最大超时未过期，因此端口应重试将 Wi-Fi 直接发送到下表中定义的相应通道上的远程设备。 表定义发出命令时，在何处发送数据包的显式通道要求。 一般规则是，响应包应在与前一个请求相同的通道上发出。

| 响应操作帧类型   | 目标传输通道                               |
|------------------------------|-------------------------------------------------------|
| 转向协商响应      | 本地侦听通道                                  |
| 转向协商确认  | 远程侦听通道                                 |
| 邀请响应          | 本地侦听或本地中转操作通道          |
| 设置发现响应 | 本地侦听通道或远程中转操作通道 |

 

当本地设备接收到发送的操作帧的确认、超时过期或主机中止操作时，任务完成。 在同一通道停留时间到期后，设备可能会指示任务完成。

主机可能决定中止此操作并继续/重试 Wi-Fi 直接操作帧交换，因此设备必须能够快速中止此操作。

## <a name="validation"></a>验证

对于支持 WDI 版本1.1.8 及更高版本的微型端口驱动程序，增加了对传出 P2P 操作帧的 P2P 的额外验证。 此验证解决了在以下情况下发生的常见问题： P2P IE 的 **配置超时** 属性（以毫秒为单位，提供给 [OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME](oid-wdi-task-p2p-send-request-action-frame.md) 和 OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME 中的 LE），到数十毫秒（这是 IE 格式）。

对于支持 WDI 版本1.1.8 和更高版本的驱动程序，如果未在传出操作帧上正确编码 P2P IE 的 **配置超时** 属性，则 Wi-Fi 直接服务和 Wi-Fi 直接服务的 HLK 测试将失败。 对于 WDI 版本1.1.7 及更早版本，测试将向测试输出输出警告。

WDI 接口本身不变，并且继续使用比在版本1.1.7 和更低版本中的毫秒数。

## <a name="task-parameters"></a>任务参数


| TLV                                                                                                               | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                                    |
|-------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 操作 \_ 帧 \_ 响应 \_ 参数**](./wdi-tlv-p2p-action-frame-response-parameters.md)   |                                |          | 参数，如操作帧类型、目标对等适配器的设备地址和对话框令牌。                                                 |
| [**WDI \_ TLV \_ P2P \_ 中转 \_ 协商 \_ 响应 \_ 信息**](./wdi-tlv-p2p-go-negotiation-response-info.md)           |                                | X        | 中转协商响应参数。 如果 wfdRequestFrameType 是 "中转协商" 响应，则该端口应仅检查此结构。            |
| [**WDI \_ TLV \_ P2P \_ 中转 \_ 协商 \_ 确认 \_ 信息**](./wdi-tlv-p2p-go-negotiation-confirmation-info.md)   |                                | X        | 中转协商确认参数。 如果 wfdRequestFrameType 是 "中转协商确认"，则该端口应仅检查此结构。    |
| [**WDI \_ TLV \_ P2P \_ 邀请 \_ 响应 \_ 信息**](./wdi-tlv-p2p-invitation-response-info.md)                    |                                | X        | 邀请响应参数。 仅当 wfdRequestFrameType 为邀请响应时，端口才能检查此结构。                   |
| [**WDI \_ TLV \_ P2P \_ 预配 \_ 发现 \_ 响应 \_ 信息**](./wdi-tlv-p2p-provision-discovery-response-info.md) |                                | X        | 预配发现响应参数。 如果 wfdRequestFrameType 是预配发现响应，则该端口只应检查此结构。 |
| [**WDI \_ TLV \_ P2P \_ 传入 \_ 帧 \_ 信息**](./wdi-tlv-p2p-incoming-frame-information.md)                |                                |          | 先前接收到的 P2P 操作帧中指出的信息。 收到的指示返回到端口。            |
| [**WDI \_ TLV \_ 供应商 \_ 特定 \_ IE**](./wdi-tlv-vendor-specific-ie.md)                                         |                                | X        | 必须包含在端口发送的帧中的一个或多个传入。                                                                           |

 

## <a name="task-completion-indication"></a>任务完成指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ P2P \_ 发送 \_ 响应 \_ 操作 \_ 帧 \_ 完成](ndis-status-wdi-indication-p2p-send-response-action-frame-complete.md)

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

 

