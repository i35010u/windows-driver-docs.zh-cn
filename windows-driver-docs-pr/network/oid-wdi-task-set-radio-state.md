---
title: OID_WDI_TASK_SET_RADIO_STATE
description: OID_WDI_TASK_SET_RADIO_STATE 用于为适配器设置的 Wi-fi 无线电的状态。
ms.assetid: d7981df2-d3e5-49fd-8414-ca350775828b
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_SET_RADIO_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 93c39173824acf545f079d3cf83095a43ca4953e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544771"
---
# <a name="oidwditasksetradiostate"></a>OID\_WDI\_TASK\_SET\_RADIO\_STATE


OID\_WDI\_任务\_设置\_单选\_状态用于为适配器设置的 Wi-fi 无线电的状态。

| 对象  | 中止支持 | 默认优先级 （主机驱动程序策略） | 正常执行时间 （秒） |
|---------|---------------|---------------------------------------|---------------------------------|
| 适配器 | 否            | 1                                     | 1                               |

 

仅在断开连接活动完成后，必须完成该任务。

IHV 组件也可能会向主机发送未经请求的单选状态更改的迹象。

主机关闭无线电之前，它断开连接所有对等节点，并停止任何正在运行的组所有者。 适配器不需要跨单选 OFF/ON 转换记住工作站/转到配置文件信息。

## <a name="task-parameters"></a>任务参数


| TLV                                                                               | 允许多个 TLV 实例 | 可选 | 描述                                                                                                           |
|-----------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_RADIO\_STATE\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/dn898043) |                                |          | 单选所需的状态。 如果此设置为 1，则启用单选。 如果此值设置为 0，单选处于关闭状态。 |

 

## <a name="task-completion-indication"></a>指示任务完成


[NDIS\_STATUS\_WDI\_INDICATION\_SET\_RADIO\_STATE\_COMPLETE](ndis-status-wdi-indication-set-radio-state-complete.md)
## <a name="unsolicited-indication"></a>未经请求的指示


[NDIS\_状态\_WDI\_指示\_单选\_状态](ndis-status-wdi-indication-radio-status.md)此指示用于报告中的适配器的单选状态的更改。 这是发送软件无线电更改触发主机时，并由适配器检测到硬件单选状态发生变化时。

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




