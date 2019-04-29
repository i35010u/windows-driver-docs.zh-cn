---
title: 系统语法
description: 系统语法
ms.assetid: f2b327cd-8ba5-45f3-9116-756df82358f4
keywords:
- 系统中，命令语法
- （系统标识符）
- 系统中，系统标识符 （）
- 有关命令，系统的语法规则
- （系统标识符） 的命令的语法规则
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4acefb5c143f880f05225fcc6b58591f32f624d5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368032"
---
# <a name="system-syntax"></a>系统语法


## <span id="ddk_system_syntax_dbg"></span><span id="DDK_SYSTEM_SYNTAX_DBG"></span>


许多调试器命令作为其参数具有进程标识符。

两个垂直条 (|) 出现在之前的系统标识符。 系统标识符可以是下列值之一。

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
<td align="left"><p>导致当前异常或调试事件系统。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>||*</strong></p></td>
<td align="left"><p>所有系统。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>||</strong><em>ddd</em></p></td>
<td align="left"><p>系统其序号<em>ddd</em>。</p></td>
</tr>
</tbody>
</table>



系统分配序号将调试器附加到它们的顺序。

当调试开始时，当前系统是导致出现异常或调试事件 （或一个到最新附加调试器）。 指定一个新的使用之前，系统都将保持在当前系统[ **| |s （设置当前系统）** ](--s--set-current-system-.md)命令或使用[进程和线程窗口](processes-and-threads-window.md)在 WinDbg 中。

<a name="example"></a>示例
-------
此示例演示三个转储文件已加载。 系统 1 处于活动状态，并且系统 2 导致调试事件。

```dbgcmd
||1:1:017> ||
   0 User mini dump: c:\notepad.dmp
.  1 User mini dump: c:\paint.dmp
#  2 User mini dump: c:\calc.dmp
```


<a name="remarks"></a>备注
-------

若要使用多个系统，可以使用[.opendump](-opendump--open-dump-file-.md)同时调试多个故障转储。 有关如何控制多个目标会话的详细信息，请参阅[调试多个目标](debugging-multiple-targets.md)。

**请注意**有采用十分复杂，在调试实时目标和转储目标组合在一起，因为每种类型的调试方式不同命令的行为时。 例如，如果您使用**g （转向）** 命令时当前系统是转储文件，调试器开始执行，但不是能中断返回到调试器，因为换行命令无法识别为有效的调试转储文件。








