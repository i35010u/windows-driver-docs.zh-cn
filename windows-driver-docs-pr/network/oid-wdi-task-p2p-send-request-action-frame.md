---
title: OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME
description: 向设备发出 OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME 以发送 Wi-Fi 直接公共操作帧请求。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 25f673d2022cd516fa0483d015754da434ab37cb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829247"
---
# <a name="oid_wdi_task_p2p_send_request_action_frame"></a>OID \_ WDI \_ 任务 \_ P2P \_ 发送 \_ 请求 \_ 操作 \_ 帧


OID \_ WDI \_ 任务 \_ P2P \_ 发送 \_ 请求 \_ 操作 \_ 帧将颁发给设备，以发送 Wi-Fi 直接公共操作帧请求。

| 对象 | 支持中止                                           | 主机驱动程序策略 (默认优先级)  | 正常执行时间 (秒)  |
|--------|---------------------------------------------------------|---------------------------------------|---------------------------------|
| 端口   | 是的。 中止后，端口必须处于干净状态。 | 3                                     | 5                               |

 

此命令不同于 [OID \_ WDI \_ 任务 \_ P2P \_ 发送 \_ 响应 \_ 操作 \_ 框架](oid-wdi-task-p2p-send-response-action-frame.md)，这是一项比较时间敏感的操作。

当设备接收到请求帧的确认时，它应停留在100ms 的同一通道上，并指示它接收到主机的任何 Wi-Fi 直接公共操作帧。

当最大超时未过期时，设备应重试将 Wi-Fi 的直接公共操作帧发送到远程设备上的侦听通道上的远程设备。

当本地设备接收到发送的操作帧的确认时，该任务就会完成，超时过期，或者主机中止操作。 在同一通道停留时间到期后，设备可能会指示任务完成。

主机可能决定中止此操作并继续/重试 Wi-Fi 直接操作帧交换，因此设备必须能够快速中止此操作。

## <a name="validation"></a>验证

对于支持 WDI 版本1.1.8 及更高版本的微型端口驱动程序，增加了对传出 P2P 操作帧的 P2P 的额外验证。 此验证解决了在以下情况下发生的常见问题： P2P IE 的 **配置超时** 属性（以毫秒为单位，提供给 OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME 和 [OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME](oid-wdi-task-p2p-send-response-action-frame.md)中的 LE），到数十毫秒（这是 IE 格式）。

对于支持 WDI 版本1.1.8 和更高版本的驱动程序，如果未在传出操作帧上正确编码 P2P IE 的 **配置超时** 属性，则 Wi-Fi 直接服务和 Wi-Fi 直接服务的 HLK 测试将失败。 对于 WDI 版本1.1.7 及更早版本，测试将向测试输出输出警告。

WDI 接口本身不变，并且继续使用比在版本1.1.7 和更低版本中的毫秒数。

## <a name="task-parameters"></a>任务参数


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>TLV</th>
<th>允许多个 TLV 实例</th>
<th>可选</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/windows-hardware/drivers/network/wdi-tlv-p2p-send-action-request-frame-parameters" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SEND_ACTION_ REQUEST_FRAME_PARAMETERS&lt;/strong&gt;](./wdi-tlv-p2p-send-action-request-frame-parameters.md)"><strong>WDI_TLV_P2P_SEND_ACTION_ REQUEST_FRAME_PARAMETERS</strong></a></td>
<td></td>
<td></td>
<td>参数，如操作帧类型、目标对等适配器的设备地址和对话框令牌。</td>
</tr>
<tr class="even">
<td><a href="/windows-hardware/drivers/network/wdi-tlv-p2p-go-negotiation-request-info" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_GO_ NEGOTIATION_REQUEST_INFO&lt;/strong&gt;](./wdi-tlv-p2p-go-negotiation-request-info.md)"><strong>WDI_TLV_P2P_GO_ NEGOTIATION_REQUEST_INFO</strong></a></td>
<td></td>
<td>X</td>
<td>中转协商请求参数。 如果 wfdRequestFrameType 是 "开始协商" 请求，则该端口应仅检查此结构。</td>
</tr>
<tr class="odd">
<td><a href="/windows-hardware/drivers/network/wdi-tlv-p2p-invitation-request-info" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INVITATION_REQUEST_INFO&lt;/strong&gt;](./wdi-tlv-p2p-invitation-request-info.md)"><strong>WDI_TLV_P2P_INVITATION_REQUEST_INFO</strong></a></td>
<td></td>
<td>X</td>
<td>邀请请求参数。 此端口仅应在 wfdRequestFrameType 为邀请请求时才检查此结构。</td>
</tr>
<tr class="even">
<td><a href="/windows-hardware/drivers/network/wdi-tlv-p2p-provision-discovery-request-info" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_PROVISION_ DISCOVERY_REQUEST_INFO&lt;/strong&gt;](./wdi-tlv-p2p-provision-discovery-request-info.md)"><strong>WDI_TLV_P2P_PROVISION_ DISCOVERY_REQUEST_INFO</strong></a></td>
<td></td>
<td>X</td>
<td>预配发现请求参数。 如果 wfdRequestFrameType 是一个预配发现请求，则该端口应仅检查此结构。</td>
</tr>
<tr class="odd">
<td><a href="/windows-hardware/drivers/network/wdi-tlv-bss-entry" data-raw-source="[&lt;strong&gt;WDI_TLV_BSS_ENTRY&lt;/strong&gt;](./wdi-tlv-bss-entry.md)"><strong>WDI_TLV_BSS_ENTRY</strong></a></td>
<td></td>
<td></td>
<td><p>从端口 Wi-Fi 直接发现任务返回的设备发现条目。</p>
<p>这样一来，端口就不需要记住其发现数据库，就可以向远程 Wi-Fi 的直接设备发送 Wi-Fi 直接操作帧请求，而无需发现。</p></td>
</tr>
<tr class="even">
<td><a href="/windows-hardware/drivers/network/wdi-tlv-vendor-specific-ie" data-raw-source="[&lt;strong&gt;WDI_TLV_VENDOR_SPECIFIC_IE&lt;/strong&gt;](./wdi-tlv-vendor-specific-ie.md)"><strong>WDI_TLV_VENDOR_SPECIFIC_IE</strong></a></td>
<td></td>
<td>X</td>
<td>必须包含在端口发送的帧中的一个或多个传入。</td>
</tr>
</tbody>
</table>

 

## <a name="task-completion-indication"></a>任务完成指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ P2P \_ 发送 \_ 请求 \_ 操作 \_ 帧 \_ 完成](ndis-status-wdi-indication-p2p-send-request-action-frame-complete.md)

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

