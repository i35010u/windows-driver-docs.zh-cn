---
title: OID_WDI_TASK_DOT11_RESET
description: OID_WDI_TASK_DOT11_RESET 请求 IHV 组件重置指定端口上的 MAC 和物理状态。
ms.assetid: 5fcac1da-0776-47a5-87b7-8e831f968f7c
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_DOT11_RESET 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: c051f1df5631ebbca54ba0e63705c38d94de7723
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383589"
---
# <a name="oidwditaskdot11reset"></a>OID\_WDI\_TASK\_DOT11\_RESET


OID\_WDI\_任务\_DOT11\_IHV 组件重置指定端口上的 MAC 和物理状态重置请求。

| Object | 中止支持 | 默认优先级 （主机驱动程序策略） | 正常执行时间 （秒） |
|--------|---------------|---------------------------------------|---------------------------------|
| 端口   | 否            | 1                                     | 1                               |

 

在发出之前 dot11 重置命令，WDI 驱动程序会停止到 IHV 组件发出新的命令和中止的端口上的正在进行中的任何任务。 它还会刷新其 Rx 和 TX 队列。

Dot11 重置组合 802.11 MLME 和 PLME 重置基元的语义。 当 IHV 组件收到 dot11 重置请求时，它应执行以下任务。

-   将端口的 MAC 实体重置为其初始状态。
-   重置，端口的 MIB 属性以便它们设置为其默认值，如果 bSetDefaultMIB 为 true。
-   重置物理实体的 TX/Rx 状态机，并将其设置为 Rx 状态仅以确保传输的帧。
-   刷新适配器的 Rx 队列并完成针对 TX 队列中每个数据包的 send。
-   如果存在 MAC 地址参数，则重置为指定的值的端口的 MAC 地址。
-   完成 dot11 重置操作之前，端口状态设置为 INIT。

如果重置的端口为 STA、 AP 或 Wi-Fi Direct 客户端或转到已运行，主机会触发断开连接任务请求要发送到对等节点重置前解除关联的 IHV 组件。 在这种情况下，IHV 组件不需要再次执行。

## <a name="task-parameters"></a>任务参数


| TLV                                                                               | 允许多个 TLV 实例 | 可选 | 描述                                       |
|-----------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------|
| [**WDI\_TLV\_DOT11\_RESET\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/dn926302) |                                |          | Dot11 重置的参数。                   |
| [**WDI\_TLV\_已配置\_MAC\_地址**](https://msdn.microsoft.com/library/windows/hardware/dn926257) |                                | X        | 应使用的端口 MAC 地址。 |

 

## <a name="task-completion-indication"></a>指示任务完成


[NDIS\_状态\_WDI\_指示\_DOT11\_重置\_完成](ndis-status-wdi-indication-dot11-reset-complete.md)

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

 

 




