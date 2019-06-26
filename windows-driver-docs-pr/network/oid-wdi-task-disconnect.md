---
title: OID_WDI_TASK_DISCONNECT
description: OID_WDI_TASK_DISCONNECT 用于终止与对等方的连接。
ms.assetid: 03566fbd-5043-4166-bd33-0ed48f85f370
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_DISCONNECT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2885a124087ee0934beaa09a7042ab145da3267d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387240"
---
# <a name="oidwditaskdisconnect"></a>OID\_WDI\_TASK\_DISCONNECT


OID\_WDI\_任务\_断开连接用于终止与对等方的连接。

| Object | 中止支持 | 默认优先级 （主机驱动程序策略） | 正常执行时间 （秒） |
|--------|---------------|---------------------------------------|---------------------------------|
| Port   | 否            | 2                                     | 1                               |

 

断开与访问点或 Wi-Fi Direct 转，以及若要断开连接的端口的客户端使用此命令。 收到断开连接后，该端口必须取消关联和 deauthenticate 从对等方并清除与该对等方关联的状态。 但是，它必须重置任何不特定于此对等方的连接参数。 仅在断开连接活动完成后，必须完成该任务。

## <a name="task-parameters"></a>任务参数


| TLV                                                                            | 允许多个 TLV 实例 | 可选 | 描述                |
|--------------------------------------------------------------------------------|--------------------------------|----------|----------------------------|
| [**WDI\_TLV\_断开连接\_参数**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-disconnect-parameters) |                                |          | 断开连接的参数。 |

 

## <a name="task-completion-indication"></a>指示任务完成


[NDIS\_状态\_WDI\_指示\_断开连接\_完成](ndis-status-wdi-indication-disconnect-complete.md)
## <a name="unsolicited-indication"></a>未经请求的指示


[NDIS\_状态\_WDI\_指示\_解除关联](ndis-status-wdi-indication-disassociation.md)时端口获取与网络断开连接，它将解除关联指示发送到操作系统。 断开连接可能会触发从操作系统中，某一命令，或从网络时可能会触发。 触发的网络断开连接可能是显式从接收到的解除关联或 deauthentication 数据包，或者端口不能检测到它连接到的对等方是否存在时不能隐式。

解除关联指示在发送之前，该端口必须清除与对等方关联的状态。 这包括任何密钥以及与对等方关联的 802.1 x 端口授权信息。 该端口不得触发其自身上的漫游。

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

 

 




