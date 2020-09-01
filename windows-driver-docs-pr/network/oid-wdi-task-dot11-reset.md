---
title: OID_WDI_TASK_DOT11_RESET
description: OID_WDI_TASK_DOT11_RESET 请求 IHV 组件将 MAC 和 PHY 状态重置为指定端口。
ms.assetid: 5fcac1da-0776-47a5-87b7-8e831f968f7c
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_DOT11_RESET 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 9d135778b4c96e1f69a6655103440195358146b6
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213199"
---
# <a name="oid_wdi_task_dot11_reset"></a>OID \_ WDI \_ TASK \_ DOT11 \_ RESET


OID \_ WDI \_ TASK \_ DOT11 \_ RESET 请求 IHV 组件将 MAC 和 PHY 状态重置为指定端口。

| 对象 | 支持中止 | 主机驱动程序策略 (默认优先级)  | 正常执行时间 (秒)  |
|--------|---------------|---------------------------------------|---------------------------------|
| 端口   | 否            | 1                                     | 1                               |

 

发出 dot11 reset 命令之前，WDI 驱动程序停止向 IHV 组件发出新的命令，并中止端口上正在进行的任何任务。 它还会刷新其 Rx 和 TX 队列。

Dot11 reset 结合了 802.11 MLME 和 PLME reset 基元的语义。 当 IHV 组件收到 dot11 reset 请求时，它应执行以下任务。

-   将端口的 MAC 实体重置为它的初始状态。
-   重置端口的 MIB 属性，以便在 bSetDefaultMIB 为 true 时将其设置为默认值。
-   重置 PHY 实体的 TX/Rx 状态机，并将其设置为 "Rx 状态"，以确保不会传输更多的帧。
-   刷新适配器的 Rx 队列，并在 TX 队列中完成每个数据包的发送。
-   如果 MAC 地址参数存在，则将该端口的 MAC 地址重置为指定的值。
-   在完成 dot11 reset 操作之前，请将端口状态设置为 INIT。

如果要重置的端口是作为 STA、AP 或 Wi-fi 直接客户端或执行的操作，主机会触发断开连接任务，请求 IHV 组件在重置前发送到对等节点。 因此，IHV 组件不需要再次执行此操作。

## <a name="task-parameters"></a>任务参数


| TLV                                                                               | 允许多个 TLV 实例 | 可选 | 说明                                       |
|-----------------------------------------------------------------------------------|--------------------------------|----------|---------------------------------------------------|
| [**WDI \_ TLV \_ DOT11 \_ 重置 \_ 参数**](./wdi-tlv-dot11-reset-parameters.md) |                                |          | Dot11 重置的参数。                   |
| [**WDI \_ TLV \_ 配置的 \_ MAC \_ 地址**](./wdi-tlv-configured-mac-address.md) |                                | X        | 端口应使用的 MAC 地址。 |

 

## <a name="task-completion-indication"></a>任务完成指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ DOT11 \_ 重置 \_ 完成](ndis-status-wdi-indication-dot11-reset-complete.md)

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

 

