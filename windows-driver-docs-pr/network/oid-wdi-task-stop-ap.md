---
title: OID_WDI_TASK_STOP_AP
description: OID_WDI_TASK_STOP_AP 请求 IHV 组件断开连接指定端口上的所有连接的客户端，并停止信标和响应探测请求。 亚太配置和 MIB 属性会保留。
ms.assetid: b7df1d2f-fed4-4079-8a2d-3f691a52ad52
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_STOP_AP 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 696230ebded716b6c11ff671e1d22b14d70e2981
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523997"
---
# <a name="oidwditaskstopap"></a>OID\_WDI\_TASK\_STOP\_AP


OID\_WDI\_任务\_停止\_AP 请求 IHV 组件断开连接指定端口上的所有已连接客户端，并停止信标和响应探测请求。 亚太配置和 MIB 属性会保留。

| 对象 | 中止支持 | 默认优先级 （主机驱动程序策略） | 正常执行时间 （秒） |
|--------|---------------|---------------------------------------|---------------------------------|
| 端口   | 否            | 2                                     | 1                               |

 

## <a name="task-parameters"></a>任务参数


无
## <a name="task-completion-indication"></a>指示任务完成


[NDIS\_状态\_WDI\_指示\_停止\_AP\_完成](ndis-status-wdi-indication-stop-ap-complete.md)要求
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

 

 




