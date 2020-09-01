---
title: OID_WDI_TASK_DISCONNECT
description: OID_WDI_TASK_DISCONNECT 用于终止与对等方的连接。
ms.assetid: 03566fbd-5043-4166-bd33-0ed48f85f370
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_DISCONNECT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d7a12839d5a16d6e5d8cfd0e3cf3a1348f51a117
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213205"
---
# <a name="oid_wdi_task_disconnect"></a>OID \_ WDI \_ TASK \_ 断开连接


OID \_ WDI \_ TASK \_ DISCONNECT 用于终止与对等方的连接。

| 对象 | 支持中止 | 主机驱动程序策略 (默认优先级)  | 正常执行时间 (秒)  |
|--------|---------------|---------------------------------------|---------------------------------|
| 端口   | 否            | 2                                     | 1                               |

 

此命令用于从接入点或 Wi-fi Direct 中转断开连接，还用于断开端口的客户端的连接。 接收到断开连接后，端口必须与对等节点解除关联和 deauthenticate，并清除与该对等方关联的状态。 但是，它不能重置不特定于此对等方的任何连接参数。 只有在断开连接活动完成后，才能完成该任务。

## <a name="task-parameters"></a>任务参数


| TLV                                                                            | 允许多个 TLV 实例 | 可选 | 说明                |
|--------------------------------------------------------------------------------|--------------------------------|----------|----------------------------|
| [**WDI \_ TLV \_ 断开 \_ 参数**](./wdi-tlv-disconnect-parameters.md) |                                |          | 断开连接参数。 |

 

## <a name="task-completion-indication"></a>任务完成指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ 断开连接 \_ 完成](ndis-status-wdi-indication-disconnect-complete.md)
## <a name="unsolicited-indication"></a>未经请求的指示


[NDIS \_状态 \_ WDI \_ 指示 \_ ](ndis-status-wdi-indication-disassociation.md) 断开端口与网络的连接时，它会将解除连接的指示发送到 OS。 断开连接可能是由操作系统中的命令触发的，也可能是从网络触发的。 网络触发的断开连接可能是从接收的解除关联或 deauthentication 数据包中显式的，或者当端口无法检测到它连接到的对等节点时，可能是隐式的。

在发送解除关联指示之前，端口必须清除与对等方关联的状态。 这包括与对等方关联的任何密钥和 802.1 x 端口授权信息。 端口不能自行触发漫游。

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

 

