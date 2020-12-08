---
title: .time（显示系统时间）
description: . Time 命令显示有关系统时间变量的信息。
keywords:
- 显示系统时间 ( 时间) 命令
- 。时间 (显示系统时间) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .time (Display System Time)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a70e7f23c74428e3fddccef361f585602cf936c0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838843"
---
# <a name="time-display-system-time"></a>.time（显示系统时间）


**. Time** 命令显示有关系统时间变量的信息。

```dbgcmd
.time [-h Hours]
```

## <a name="span-idddk_meta_display_system_time_dbgspanspan-idddk_meta_display_system_time_dbgspanparameters"></a><span id="ddk_meta_display_system_time_dbg"></span><span id="DDK_META_DISPLAY_SYSTEM_TIME_DBG"></span>参数


<span id="_______-h________Hours______"></span><span id="_______-h________hours______"></span><span id="_______-H________HOURS______"></span>**-h**  **** *小时*   
指定格林尼治标准时间的偏移量（以小时为单位）。 负值 *值必须括* 在括号中。

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
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p>目标</p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p>平台</p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

系统时间变量控制性能计数器的行为。

下面是内核模式的示例：

```dbgcmd
kd> .time
Debug session time: Wed Jan 31 14:47:08 2001
System Uptime: 0 days 2:53:56 
```

下面是用户模式的示例：

```dbgcmd
0:000> .time
Debug session time: Mon Apr 07 19:10:50 2003
System Uptime: 4 days 4:53:56.461
Process Uptime: 0 days 0:00:08.750
  Kernel time: 0 days 0:00:00.015
  User time: 0 days 0:00:00.015
```

 

 





