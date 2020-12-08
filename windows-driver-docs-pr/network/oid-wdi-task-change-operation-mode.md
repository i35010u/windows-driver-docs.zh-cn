---
title: OID_WDI_TASK_CHANGE_OPERATION_MODE
description: OID_WDI_TASK_CHANGE_OPERATION_MODE 配置端口的操作模式。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_CHANGE_OPERATION_MODE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d636365e7b878edad102735470fa9b7411275cc3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829311"
---
# <a name="oid_wdi_task_change_operation_mode"></a>OID \_ WDI \_ 任务 \_ 更改 \_ 操作 \_ 模式


OID \_ WDI \_ 任务 \_ 更改 \_ 操作 \_ 模式配置端口的操作模式。

| 对象 | 支持中止 | 主机驱动程序策略 (默认优先级)  | 正常执行时间 (秒)  |
|--------|---------------|---------------------------------------|---------------------------------|
| 端口   | 否            | 4                                     | 1                               |

 

## <a name="task-parameters"></a>任务参数


| TLV                                                              | 允许多个 TLV 实例 | 可选 | 说明                 |
|------------------------------------------------------------------|--------------------------------|----------|-----------------------------|
| [**WDI \_ TLV \_ 操作 \_ 模式**](./wdi-tlv-operation-mode.md) |                                |          | 所需操作模式。 |

 

## <a name="task-completion-indication"></a>任务完成指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ 更改 \_ 操作 \_ 模式 \_ 完成](ndis-status-wdi-indication-change-operation-mode-complete.md)

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

 

