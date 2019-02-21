---
title: 如果
description: 如果令牌的行为类似于 if 关键字在 C 中
ms.assetid: ccd74461-759f-400d-90da-efba2e4498e6
keywords:
- 如果 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .if
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1dfb6195be3945914fd5d119c53c2607baac7e6f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534429"
---
# <a name="if"></a>如果


**.If**令牌的行为类似于**如果**在 C 中的关键字

```dbgcmd
.if (Condition) { Commands } 

.if (Condition) { Commands } .else { Commands } 

.if (Condition) { Commands } .elsif (Condition) { Commands } 

.if (Condition) { Commands } .elsif (Condition) { Commands } .else { Commands } 
```

## <a name="span-idddktokenifdbgspanspan-idddktokenifdbgspansyntax-elements"></a><span id="ddk_token_if_dbg"></span><span id="DDK_TOKEN_IF_DBG"></span>语法元素


<span id="_______Condition______"></span><span id="_______condition______"></span><span id="_______CONDITION______"></span> *Condition*   
指定的条件。 如果此计算结果为零，则将其视为 false;否则为 true。 封闭*条件*在括号是可选的。 *条件*必须是一个表达式，而不是调试器命令。 它将由默认表达式计算器 （MASM 或 c + +） 进行评估。 有关详细信息，请参阅[数值表达式语法](numerical-expression-syntax.md)。

<span id="_______Commands______"></span><span id="_______commands______"></span><span id="_______COMMANDS______"></span> *命令*   
指定一个或多个命令将有条件地执行。 下面的命令块必须括在大括号，即使它包含单个命令。 之前的右大括号不需要后接分号，应由分号，但最后一个命令分隔的多个命令。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关其他控制流令牌在调试器命令程序及其用法的信息，请参阅[使用调试器命令程序](using-debugger-command-programs.md)。

 

 





