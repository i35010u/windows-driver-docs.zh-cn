---
title: for_each_local
description: For_each_local 扩展对当前帧中的每个局部变量执行一次调试器命令。
keywords:
- for_each_local Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- for_each_local
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b0be9947b018c7f1f76bf8ef2cfab16d4a4d0a9a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822655"
---
# <a name="for_each_local"></a>！对于 \_ 每个 \_ 本地


**对于 \_ 每个本地扩展，每个 \_ 本地** 扩展对当前帧中的每个局部变量执行一次调试器命令。

```dbgcmd
!for_each_local ["CommandString"] 
!for_each_local -? 
```

## <a name="span-idddk__for_each_local_dbgspanspan-idddk__for_each_local_dbgspanparameters"></a><span id="ddk__for_each_local_dbg"></span><span id="DDK__FOR_EACH_LOCAL_DBG"></span>参数


<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span>*Command.commandstring*   
指定为当前堆栈帧中的每个局部变量执行一次的调试器命令。 如果 *command.commandstring* 包含多个命令，则必须用分号分隔它们，并将 *command.commandstring* 括在引号中。 如果包含多个命令，则 *command.commandstring* 中的单个命令不能包含引号。

在 *command.commandstring* 中，或在 *command.commandstring* 执行命令的任何脚本中，可以使用 **@ \# 本地** 别名。 此别名替换为本地变量的名称。 此替换在执行 *command.commandstring* 之前和进行任何其他分析之前发生。 此别名区分大小写，必须在其前面加一个空格并在其后面添加一个空格，即使将该别名括在括号中。 如果使用 c + + 表达式语法，则必须以 **@ @ ( @ \# Local )** 的形式引用此别名。

此别名仅在对 **\_ 每个 \_ 本地** 的调用的生存期内可用。 不要将此别名与伪寄存器、固定名称别名或用户命名别名混淆。

<span id="_______-_______"></span> **-?**   
在 [调试器命令窗口](debugger-command-window.md)中显示此扩展的一些帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何显示和更改局部变量的详细信息，以及其他与内存相关的命令的说明，请参阅 [读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

如果未指定任何参数，则 **\_ 每个 \_ 本地** 扩展的！会列出局部变量。 有关局部变量的详细信息，请使用 [**dv (在) 命令中显示局部变量**](dv--display-local-variables-.md) 。

如果启用 "详细调试器输出"，则在调用该扩展时，显示将包含局部变量总数，并且每次对本地变量执行 *command.commandstring* 时，该变量和 *command.commandstring* 的文本都将被回显。

 

 





