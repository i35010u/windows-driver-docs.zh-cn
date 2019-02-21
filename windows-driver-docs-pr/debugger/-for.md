---
title: .for
description: 。 有关令牌的行为类似于在 C 中的关键字，除该多个增量命令必须以分号分隔，不是逗号。
ms.assetid: 35f54c4c-e7f5-42a9-b579-1e4958b7286b
keywords:
- 。 有关 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .for
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 09e3d3fc802c7a81aa9e1564a1bb7ee6f6d52fd0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544248"
---
# <a name="for"></a>.for


**。 有关**令牌的行为类似于**为**关键字在 C 中，不同之处的多个增量命令必须用分号分隔，不是由逗号分隔。

```dbgcmd
.for (InitialCommand ; Condition ; IncrementCommands) { Commands } 
```

## <a name="span-idddktokenfordbgspanspan-idddktokenfordbgspansyntax-elements"></a><span id="ddk_token_for_dbg"></span><span id="DDK_TOKEN_FOR_DBG"></span>语法元素


<span id="_______InitialCommand______"></span><span id="_______initialcommand______"></span><span id="_______INITIALCOMMAND______"></span> *InitialCommand*   
指定将在循环开始之前执行的命令。 允许单个初始命令。

<span id="_______Condition______"></span><span id="_______condition______"></span><span id="_______CONDITION______"></span> *Condition*   
指定的条件。 如果此计算结果为零，则将其视为 false;否则为 true。 封闭*条件*在括号是可选的。 *条件*必须是一个表达式，而不是调试器命令。 它将由默认表达式计算器 （MASM 或 c + +） 进行评估。 有关详细信息，请参阅[数值表达式语法](numerical-expression-syntax.md)。

<span id="_______IncrementCommands______"></span><span id="_______incrementcommands______"></span><span id="_______INCREMENTCOMMANDS______"></span> *IncrementCommands*   
指定将在每个循环结束执行的一个或多个命令。 如果你想要使用多个增量命令，用分号分隔它们，但不将它们放在大括号中。

<span id="_______Commands______"></span><span id="_______commands______"></span><span id="_______COMMANDS______"></span> *命令*   
指定一个或多个命令将重复执行，只要条件为 true。 下面的命令块必须括在大括号，即使它包含单个命令。 之前的右大括号不需要后接分号，应由分号，但最后一个命令分隔的多个命令。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关其他控制流令牌在调试器命令程序及其用法的信息，请参阅[使用调试器命令程序](using-debugger-command-programs.md)。

<a name="remarks"></a>备注
-------

如果所有工作都由增量命令正在都完成，则可以省略*条件*完全且只需使用一对空大括号。

下面是举例 **。 有关**语句包含多个增量命令：

```dbgcmd
0:000> .for (r eax=0; @eax < 7; r eax=@eax+1; r ebx=@ebx+1) { .... }
```

[ **.Break** ](https://msdn.microsoft.com/library/windows/hardware/ff556242)并[ **.continue** ](-continue.md)令牌可用于退出或重新启动*命令*块。

 

 





