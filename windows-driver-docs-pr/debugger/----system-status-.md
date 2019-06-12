---
title: （系统状态）
description: （） 命令栏的双精度垂直打印指定的系统或当前正在调试的所有系统的状态。不要混淆此命令使用 （进程状态） 命令。
ms.assetid: fcea61b1-2ec5-4c80-abd7-269b95d56cd4
keywords:
- （系统状态）Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- (System Status)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8e9c35c30ae28f7610712d02c114f19aa2b24027
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337067"
---
# <a name="-system-status"></a>||（系统状态）


双竖线 ( **||** ) 命令将打印指定的系统或当前正在调试的所有系统的状态。

不要将使用此命令相混淆[ **|（进程状态）** ](---process-status-.md)命令。

```dbgcmd
|| System 
```

## <a name="span-idddkcmdsystemstatusdbgspanspan-idddkcmdsystemstatusdbgspanparameters"></a><span id="ddk_cmd_system_status_dbg"></span><span id="DDK_CMD_SYSTEM_STATUS_DBG"></span>参数


<span id="_______System______"></span><span id="_______system______"></span><span id="_______SYSTEM______"></span> *System*   
指定要显示的系统。 如果省略此参数，将显示正在调试的所有系统。 有关语法的详细信息，请参阅[系统语法](system-syntax.md)。

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

**||** 命令仅在调试多个目标很有用。 很多，但并非所有的多个目标调试会话涉及多个系统。 有关这些会话的详细信息，请参阅[调试多个目标](debugging-multiple-targets.md)。

每个系统列表包括服务器名称和协议详细信息。 系统上运行调试器都会被视为 **&lt;本地&gt;** 。

下面的示例显示如何使用此命令。 下面的命令显示所有系统。

```dbgcmd
3:2:005> ||
```

以下命令还显示所有系统。

```dbgcmd
3:2:005> ||*
```

下面的命令显示当前处于活动状态的系统。

```dbgcmd
3:2:005> ||.
```

下面的命令显示系统中有最新的异常或中断。

```dbgcmd
3:2:005> ||#
```

下面的命令显示系统编号 2。

```dbgcmd
3:2:005> ||2
```

 

 





