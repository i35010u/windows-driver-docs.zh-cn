---
title: s （当前系统设置）
description: S 命令设置或显示当前的系统数。
ms.assetid: 33ad3a63-166f-4669-868c-49100c9b4d8c
keywords:
- s （当前系统设置） Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- s (Set Current System)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6079bff9140a042410252a0ecbee5da5eca6569f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337075"
---
# <a name="s-set-current-system"></a>||s（设置当前系统）

**| |s**命令设置或显示当前的系统数。

```dbgcmd
     ||System s 
     || s 
```

不要将使用此命令相混淆[ **s （内存搜索）**](s--search-memory-.md)， [ **~ s （更改当前处理器）**](-s--change-current-processor-.md)， [ **~ （设置当前线程） s**](-s--set-current-thread-.md)，或[ **| s （设置当前进程）** ](-s--set-current-process-.md)命令。


## <a name="span-idddkcmdsetcurrentsystemdbgspanspan-idddkcmdsetcurrentsystemdbgspanparameters"></a><span id="ddk_cmd_set_current_system_dbg"></span><span id="DDK_CMD_SET_CURRENT_SYSTEM_DBG"></span>参数


<span id="_______System______"></span><span id="_______system______"></span><span id="_______SYSTEM______"></span> *System*   
指定要激活的系统编号。 有关语法的详细信息，请参阅[系统语法](system-syntax.md)。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>调试多个目标</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**| |s**调试多个目标或使用多个转储文件时，命令很有用。  有关这些类型的会话的详细信息，请参阅[调试多个目标](debugging-multiple-targets.md)。

如果使用 **| |s**语法，调试器将显示有关当前系统的信息。

此命令还将分解为当前系统、 进程和线程的当前指令。

 
**请注意**  有采用十分复杂，在调试实时目标和转储目标组合在一起，因为每种类型的调试方式不同命令的行为时。 例如，如果您使用**g （转向）** 命令时当前系统是转储文件，调试器开始执行，但不是能中断返回到调试器，因为换行命令无法识别为有效的调试转储文件。









