---
title: OID_WDI_TASK_OPEN
description: OID_WDI_TASK_OPEN 要求 IHV 组件初始化适配器。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_OPEN 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: f5d4bc3f3992e67cdc2f9321c68ef85164c4556b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829265"
---
# <a name="oid_wdi_task_open"></a>OID \_ WDI \_ 任务 \_ 打开


OID \_ WDI \_ 任务 \_ 打开请求 IHV 组件初始化适配器。

| 对象  | 支持中止 | 主机驱动程序策略 (默认优先级)  | 正常执行时间 (秒)  |
|---------|---------------|---------------------------------------|---------------------------------|
| 适配器 | 否            | 1                                     | 2                               |

 

适配器初始化包括将固件下载到适配器、设置中断和其他硬件资源。 在初始化期间，此任务使用由 IHV 注册的 OpenAdapterHandler 处理程序传递到 IHV。 从低功耗状态恢复时，此功能将使用 OID \_ WDI TASK OPEN 传递到 IHV \_ \_ 。

## <a name="task-parameters"></a>任务参数


无
## <a name="task-completion-indication"></a>任务完成指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ 打开 \_ 完成](ndis-status-wdi-indication-open-complete.md)

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

 

 




