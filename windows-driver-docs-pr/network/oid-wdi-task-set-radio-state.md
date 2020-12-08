---
title: OID_WDI_TASK_SET_RADIO_STATE
description: OID_WDI_TASK_SET_RADIO_STATE 用于设置适配器的 Wi-Fi 无线电状态。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_SET_RADIO_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 80bc8e4647d6f386e8b7404b1dcc2f0cdc6b0412
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829219"
---
# <a name="oid_wdi_task_set_radio_state"></a>OID \_ WDI \_ 任务 \_ 集 \_ 无线电 \_ 状态


OID \_ WDI \_ 任务 \_ 集 \_ 收音机 \_ 状态用于设置适配器的 Wi-Fi 无线电状态。

| 对象  | 支持中止 | 主机驱动程序策略 (默认优先级)  | 正常执行时间 (秒)  |
|---------|---------------|---------------------------------------|---------------------------------|
| 适配器 | 否            | 1                                     | 1                               |

 

只有在断开连接活动完成后，才能完成该任务。

IHV 组件还可以向主机发送有关无线电状态更改的未经请求的指示。

在主机关闭收音机之前，它会断开所有对等节点的连接，并停止正在运行的任何组所有者。 适配器不应在无线电关/转换时记住工作站/转型配置文件信息。

## <a name="task-parameters"></a>任务参数


| TLV                                                                               | 允许多个 TLV 实例 | 可选 | 说明                                                                                                           |
|-----------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ 无线电 \_ 状态 \_ 参数**](./wdi-tlv-radio-state-parameters.md) |                                |          | 广播的所需状态。 如果此设置为1，则启用无线电。 如果此设置为0，则关闭无线电。 |

 

## <a name="task-completion-indication"></a>任务完成指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ 设置的 \_ 无线电 \_ 状态已 \_ 完成](ndis-status-wdi-indication-set-radio-state-complete.md)
## <a name="unsolicited-indication"></a>未经请求的指示


[NDIS \_状态 \_ WDI \_ 指示 \_ 无线电 \_ 状态](ndis-status-wdi-indication-radio-status.md) 此指示用于报告适配器的无线电状态更改。 当主机触发软件无线电更改并且适配器检测到硬件无线电状态更改时，将同时发送此项。

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

 

