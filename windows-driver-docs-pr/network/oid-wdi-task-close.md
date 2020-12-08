---
title: OID_WDI_TASK_CLOSE
description: OID_WDI_TASK_CLOSE 要求 IHV 组件关闭适配器。 这包括禁用中断和关闭硬件。 暂停期间，此任务通过 IHV 注册的 CloseAdapterHandler 处理程序传递到 IHV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_CLOSE 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 9616eda4745b67d267fcf13570a1788da14e12a0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829285"
---
# <a name="oid_wdi_task_close"></a>OID \_ WDI \_ 任务 \_ 关闭


OID \_ WDI \_ 任务 \_ 关闭请求 IHV 组件关闭适配器。 这包括禁用中断和关闭硬件。 暂停期间，此任务通过 IHV 注册的 CloseAdapterHandler 处理程序传递到 IHV。

| 对象  | 支持中止 | 主机驱动程序策略 (默认优先级)  | 正常执行时间 (秒)  |
|---------|---------------|---------------------------------------|---------------------------------|
| 适配器 | 否            | 1                                     | 5                               |

 

## <a name="task-parameters"></a>任务参数


无
## <a name="task-completion-indication"></a>任务完成指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ 关闭 \_ 完成](ndis-status-wdi-indication-close-complete.md)

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

 

 




