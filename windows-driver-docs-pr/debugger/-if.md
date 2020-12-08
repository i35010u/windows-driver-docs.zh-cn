---
title: .if
description: 如果标记在 C 中的行为类似于 if 关键字，则为。
keywords:
- 。如果 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .if
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 311b452d24a08cbd38215c1ffe0704803215e86a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799869"
---
# <a name="if"></a>.if


如果标记在 C 中的行为类似于 **if** 关键字，则为 **。**

```dbgcmd
.if (Condition) { Commands } 

.if (Condition) { Commands } .else { Commands } 

.if (Condition) { Commands } .elsif (Condition) { Commands } 

.if (Condition) { Commands } .elsif (Condition) { Commands } .else { Commands } 
```

## <a name="span-idddk_token_if_dbgspanspan-idddk_token_if_dbgspansyntax-elements"></a><span id="ddk_token_if_dbg"></span><span id="DDK_TOKEN_IF_DBG"></span>语法元素


<span id="_______Condition______"></span><span id="_______condition______"></span><span id="_______CONDITION______"></span>*条件*   
指定条件。 如果此值为零，则将其视为 false;否则为 true。 括号中的封闭 *条件* 是可选的。 *Condition* 必须是表达式，而不能是调试器命令。 它将通过默认表达式计算器 (MASM 或 c + +) 进行计算。 有关详细信息，请参阅 [数值表达式语法](numerical-expression-syntax.md)。

<span id="_______Commands______"></span><span id="_______commands______"></span><span id="_______COMMANDS______"></span>*命令*   
指定一个或多个将有条件执行的命令。 此命令块需要括在大括号中，即使它包含单个命令也是如此。 应该用分号分隔多个命令，但右大括号前的最后一个命令无需后跟分号。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关其他控制流令牌及其在调试器命令程序中的使用的信息，请参阅 [使用调试器命令程序](using-debugger-command-programs.md)。

 

 





