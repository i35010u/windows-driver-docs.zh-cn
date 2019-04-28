---
title: .time（显示系统时间）
description: .Time 命令显示有关系统时间变量的信息。
ms.assetid: d8024f84-98ff-4017-81c5-8a08973f9e4b
keywords:
- 显示系统时间 (.time) 命令
- .time （显示系统时间） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .time (Display System Time)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5c368099fceda7d57bc51d0509de68e391b30a40
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334225"
---
# <a name="time-display-system-time"></a>.time（显示系统时间）


**.Time**命令显示有关系统时间变量信息。

```dbgcmd
.time [-h Hours]
```

## <a name="span-idddkmetadisplaysystemtimedbgspanspan-idddkmetadisplaysystemtimedbgspanparameters"></a><span id="ddk_meta_display_system_time_dbg"></span><span id="DDK_META_DISPLAY_SYSTEM_TIME_DBG"></span>参数


<span id="_______-h________Hours______"></span><span id="_______-h________hours______"></span><span id="_______-H________HOURS______"></span> **-h** **** *小时*   
以小时为单位指定格林尼治标准时间，偏移量。 值为负*小时*必须括在括号中。

<span></span>  

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>模式</p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p>目标</p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p>平台</p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统时间变量控制性能计数器行为。

下面是在内核模式下的示例：

```dbgcmd
kd> .time
Debug session time: Wed Jan 31 14:47:08 2001
System Uptime: 0 days 2:53:56 
```

下面是在用户模式下的一个示例：

```dbgcmd
0:000> .time
Debug session time: Mon Apr 07 19:10:50 2003
System Uptime: 4 days 4:53:56.461
Process Uptime: 0 days 0:00:08.750
  Kernel time: 0 days 0:00:00.015
  User time: 0 days 0:00:00.015
```

 

 





