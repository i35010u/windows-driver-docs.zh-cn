---
title: OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME
description: OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME 颁发给 IHV 组件以将 Wi-Fi Direct 公共操作框架请求发送到对等方。
ms.assetid: 5cb57f20-ef9d-4e79-9b4b-8cf939221d47
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bde0588d67588e7f6e7ca28a97986a647005444a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556013"
---
# <a name="oidwditaskp2psendresponseactionframe"></a>OID\_WDI\_TASK\_P2P\_SEND\_RESPONSE\_ACTION\_FRAME


OID\_WDI\_任务\_P2P\_发送\_响应\_操作\_帧颁发给 IHV 组件以将 Wi-Fi Direct 公共操作框架请求发送到对等方。

| 对象 | 中止支持                                           | 默认优先级 （主机驱动程序策略） | 正常执行时间 （秒） |
|--------|---------------------------------------------------------|---------------------------------------|---------------------------------|
| 端口   | 是。 端口必须保持干净状态后中止。 | 3                                     | 5                               |

 

当端口收到的确认请求帧时，它应会仔细斟酌在同一个通道上为 100 毫秒，并指示任何 Wi-Fi Direct 公共操作帧它接收到的主机。

此任务是时间敏感。 Wi-Fi Direct 规范要求，发送 Wi-Fi Direct 操作响应仅提供服务的接收此数据包 100 毫秒内。

而最大超时时间尚未过期，该端口应向发送重试 Wi-Fi Direct 适当的信道上的远程设备由下表定义。 此表定义的显式通道要求，可向其发送数据包时发出此命令。 一般规则是应在先前的请求作为同一个通道上发送的响应数据包。

| 响应操作框架类型   | 目标传输通道                               |
|------------------------------|-------------------------------------------------------|
| 转协商响应      | 本地侦听通道                                  |
| 转协商确认  | 远程侦听通道                                 |
| 邀请响应          | 本地侦听或本地转到操作通道          |
| 配置发现响应 | 本地侦听通道或远程 GO 操作通道 |

 

任务已完成或者本地设备从远程设备操作帧发送接收确认时，在超时到期，或主机中止操作。 同一个通道停留时间过期后，设备可能表示任务完成。

主机可能会决定中止此操作并继续/重试 Wi-Fi Direct 操作帧 exchange，因此，必须在设备是能够快速中止此操作。

## <a name="task-parameters"></a>任务参数


| TLV                                                                                                               | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                    |
|-------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_ACTION\_FRAME\_RESPONSE\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/dn897859)   |                                |          | 参数，如操作帧类型，目标对等方适配器和对话框令牌的设备地址。                                                 |
| [**WDI\_TLV\_P2P\_GO\_NEGOTIATION\_RESPONSE\_INFO**](https://msdn.microsoft.com/library/windows/hardware/dn897942)           |                                | X        | 请转协商响应参数。 如果 wfdRequestFrameType 转协商响应，该端口应仅检查此结构。            |
| [**WDI\_TLV\_P2P\_转\_协商\_确认\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn897880)   |                                | X        | 请转协商确认参数。 如果 wfdRequestFrameType 转协商确认消息，该端口应只能检查此结构。    |
| [**WDI\_TLV\_P2P\_邀请\_响应\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn897968)                    |                                | X        | 邀请响应参数。 如果 wfdRequestFrameType 是邀请的响应，该端口仅应检查此结构。                   |
| [**WDI\_TLV\_P2P\_预配\_发现\_响应\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn897983) |                                | X        | 预配发现响应参数。 如果 wfdRequestFrameType 是配置发现响应，该端口仅应检查此结构。 |
| [**WDI\_TLV\_P2P\_传入\_帧\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn897957)                |                                |          | 但指定从以前接收的 P2P 操作帧的信息。 接收的指示提供返回到该端口。            |
| [**WDI\_TLV\_VENDOR\_SPECIFIC\_IE**](https://msdn.microsoft.com/library/windows/hardware/dn898076)                                         |                                | X        | 必须包含在由端口发送帧的一个或多个 Ie。                                                                           |

 

## <a name="task-completion-indication"></a>指示任务完成


[NDIS\_状态\_WDI\_指示\_P2P\_发送\_响应\_操作\_帧\_完成](ndis-status-wdi-indication-p2p-send-response-action-frame-complete.md)要求
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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




