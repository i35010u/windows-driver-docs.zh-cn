---
title: OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME
description: OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME 颁发给设备的 Wi-Fi Direct 公共操作框架请求发送。
ms.assetid: bd8a746e-7d47-44c1-ad05-a452ce00749f
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 48b49b8c11dc91aaca2297727f927f5a8338a9d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555616"
---
# <a name="oidwditaskp2psendrequestactionframe"></a>OID\_WDI\_TASK\_P2P\_SEND\_REQUEST\_ACTION\_FRAME


OID\_WDI\_任务\_P2P\_发送\_请求\_操作\_帧颁发给设备的 Wi-Fi Direct 公共操作框架请求发送。

| 对象 | 中止支持                                           | 默认优先级 （主机驱动程序策略） | 正常执行时间 （秒） |
|--------|---------------------------------------------------------|---------------------------------------|---------------------------------|
| 端口   | 是。 端口必须保持干净状态后中止。 | 3                                     | 5                               |

 

此命令是不同于[OID\_WDI\_任务\_P2P\_发送\_响应\_操作\_帧](oid-wdi-task-p2p-send-response-action-frame.md)，这是显著更多的时间敏感型操作。

当设备收到请求帧的确认时，它应会仔细斟酌在同一个通道上为 100 毫秒，并指示任何 Wi-Fi Direct 公共操作帧它接收到的主机。

而最大超时时间尚未过期，设备应重试发送到远程设备的侦听通道上的远程设备的 Wi-Fi Direct 公共操作帧。

任务已完成或者本地设备从远程设备操作帧发送接收确认时，在超时到期，或主机中止操作。 同一个通道停留时间过期后，设备可能表示任务完成。

主机可能会决定中止此操作并继续/重试 Wi-Fi Direct 操作帧 exchange，因此，必须在设备是能够快速中止此操作。

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
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898001" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SEND_ACTION_ REQUEST_FRAME_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898001)"><strong>WDI_TLV_P2P_SEND_ACTION_ REQUEST_FRAME_PARAMETERS</strong></a></td>
<td></td>
<td></td>
<td>参数，如操作帧类型，目标对等方适配器和对话框令牌的设备地址。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897937" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_GO_ NEGOTIATION_REQUEST_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897937)"><strong>WDI_TLV_P2P_GO_ NEGOTIATION_REQUEST_INFO</strong></a></td>
<td></td>
<td>X</td>
<td>请转协商请求参数。 如果 wfdRequestFrameType 转协商请求，该端口仅应检查此结构。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897963" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INVITATION_REQUEST_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897963)"><strong>WDI_TLV_P2P_INVITATION_REQUEST_INFO</strong></a></td>
<td></td>
<td>X</td>
<td>邀请请求参数。 如果 wfdRequestFrameType 是邀请请求，该端口仅应检查此结构。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897980" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_PROVISION_ DISCOVERY_REQUEST_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897980)"><strong>WDI_TLV_P2P_PROVISION_ DISCOVERY_REQUEST_INFO</strong></a></td>
<td></td>
<td>X</td>
<td>预配发现请求参数。 如果 wfdRequestFrameType 是预配发现请求，该端口仅应检查此结构。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926162" data-raw-source="[&lt;strong&gt;WDI_TLV_BSS_ENTRY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926162)"><strong>WDI_TLV_BSS_ENTRY</strong></a></td>
<td></td>
<td></td>
<td><p>设备发现条目从端口由 Wi-Fi Direct 发现任务返回。</p>
<p>提供，因此不需要记住其发现的数据库以将 Wi-Fi Direct 操作框架请求发送到远程 Wi-Fi Direct 设备，而无需为在发现端口。</p></td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898076" data-raw-source="[&lt;strong&gt;WDI_TLV_VENDOR_SPECIFIC_IE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898076)"><strong>WDI_TLV_VENDOR_SPECIFIC_IE</strong></a></td>
<td></td>
<td>X</td>
<td>必须包含在由端口发送帧的一个或多个 Ie。</td>
</tr>
</tbody>
</table>

 

## <a name="task-completion-indication"></a>指示任务完成


[NDIS\_状态\_WDI\_指示\_P2P\_发送\_请求\_操作\_帧\_完成](ndis-status-wdi-indication-p2p-send-request-action-frame-complete.md)要求
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

 

 




