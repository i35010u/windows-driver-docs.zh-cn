---
title: 系统语法
description: 系统语法
keywords:
- 系统，命令语法
- " (系统标识符) "
- '系统、系统标识符 ( ) '
- 命令、系统的语法规则
- '命令的语法规则， (系统标识符) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4875809c5e4ed971162300dab6b263ac285f4f6c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833161"
---
# <a name="system-syntax"></a>系统语法


## <span id="ddk_system_syntax_dbg"></span><span id="DDK_SYSTEM_SYNTAX_DBG"></span>


许多调试器命令都将进程标识符作为其参数。

两条竖线 ( | |) 出现在系统标识符之前。 系统标识符可以是下列值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">系统标识符</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>||.</strong></p></td>
<td align="left"><p>当前系统</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>||#</strong></p></td>
<td align="left"><p>导致当前异常或调试事件的系统。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>||*</strong></p></td>
<td align="left"><p>所有系统。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>||</strong><em>ddd</em></p></td>
<td align="left"><p>序数为 <em>ddd</em>的系统。</p></td>
</tr>
</tbody>
</table>



系统会按调试器附加到的顺序分配顺序。

当调试开始时，当前系统是导致当前异常或调试事件 (或调试器最近附加到) 的系统。 该系统将保留当前系统，直到你使用 [**| |s (设置当前系统)**](--s--set-current-system-.md) 命令或使用 WinDbg 中的 " [进程" 和 "线程" 窗口](processes-and-threads-window.md) 。

<a name="example"></a>示例
-------
此示例显示了三个转储文件。 系统1处于活动状态，而系统2导致了调试事件。

```dbgcmd
||1:1:017> ||
   0 User mini dump: c:\notepad.dmp
.  1 User mini dump: c:\paint.dmp
#  2 User mini dump: c:\calc.dmp
```


<a name="remarks"></a>备注
-------

若要使用多个系统，可以使用 [opendump](-opendump--open-dump-file-.md) 来同时调试多个故障转储。 有关如何控制多目标会话的详细信息，请参阅 [调试多个目标](debugging-multiple-targets.md)。

**注意**   在调试实时目标并将目标转储到一起时，有一些复杂的问题，因为每种调试类型的命令的行为有所不同。 例如，如果在当前系统为转储文件时使用 **g (中转)** 命令，则调试器将开始执行，但无法中断到调试器中，因为 break 命令未被识别为对转储文件调试无效。








