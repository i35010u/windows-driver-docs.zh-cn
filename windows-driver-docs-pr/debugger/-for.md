---
title: .for
description: 的. for 标记的行为类似于 C 中的 for 关键字，只不过多个增量命令必须用分号（而不是逗号）分隔。
keywords:
- 。对于 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .for
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3d13bbc7ba940159b556d8d0303e8ddc515d18e2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815499"
---
# <a name="for"></a>.for


的 **. for** 标记的行为类似于 C 中的 **for** 关键字，只不过多个增量命令必须用分号（而不是逗号）分隔。

```dbgcmd
.for (InitialCommand ; Condition ; IncrementCommands) { Commands } 
```

## <a name="span-idddk_token_for_dbgspanspan-idddk_token_for_dbgspansyntax-elements"></a><span id="ddk_token_for_dbg"></span><span id="DDK_TOKEN_FOR_DBG"></span>语法元素


<span id="_______InitialCommand______"></span><span id="_______initialcommand______"></span><span id="_______INITIALCOMMAND______"></span>*InitialCommand*   
指定将在循环开始之前执行的命令。 只允许一个初始命令。

<span id="_______Condition______"></span><span id="_______condition______"></span><span id="_______CONDITION______"></span>*条件*   
指定条件。 如果此值为零，则将其视为 false;否则为 true。 括号中的封闭 *条件* 是可选的。 *Condition* 必须是表达式，而不能是调试器命令。 它将通过默认表达式计算器 (MASM 或 c + +) 进行计算。 有关详细信息，请参阅 [数值表达式语法](numerical-expression-syntax.md)。

<span id="_______IncrementCommands______"></span><span id="_______incrementcommands______"></span><span id="_______INCREMENTCOMMANDS______"></span>*IncrementCommands*   
指定将在每个循环结束时执行的一个或多个命令。 如果要使用多个增量命令，请用分号分隔它们，但不要将它们括在大括号中。

<span id="_______Commands______"></span><span id="_______commands______"></span><span id="_______COMMANDS______"></span>*命令*   
指定一个或多个命令，只要条件为 true，就会重复执行这些命令。 此命令块需要括在大括号中，即使它包含单个命令也是如此。 应该用分号分隔多个命令，但右大括号前的最后一个命令无需后跟分号。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关其他控制流令牌及其在调试器命令程序中的使用的信息，请参阅 [使用调试器命令程序](using-debugger-command-programs.md)。

<a name="remarks"></a>备注
-------

如果所有工作都是通过增量命令完成的，则可以完全省略 *条件* ，只需使用一对大括号即可。

下面是一个的示例 **。 for** 语句包含多个增量命令：

```dbgcmd
0:000> .for (r eax=0; @eax < 7; r eax=@eax+1; r ebx=@ebx+1) { .... }
```

[**Break**](https://support.microsoft.com/help/833721/available-switch-options-for-the-windows-xp-and-the-windows-server-200)和 [**. continue**](-continue.md)标记可用于退出或重新启动 *命令* 块。

 

