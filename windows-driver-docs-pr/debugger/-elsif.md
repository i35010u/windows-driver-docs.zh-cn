---
title: .elsif
description: .Elsif 令牌的行为类似于其他如果在 C 中的关键字组合
ms.assetid: f5612326-9fcf-4f2e-9692-cc75e7ff4664
keywords:
- .elsif Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .elsif
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5e4c5ab3f18f7867f0b47c63e3251aa62028ae6e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334528"
---
# <a name="elsif"></a>.elsif


**.Elsif**令牌的行为类似于**的 else if**在 C 中的关键字组合

```dbgcmd
.if (Condition) { Commands } .elsif (Condition) { Commands } 

.if (Condition) { Commands } .elsif (Condition) { Commands } .else { Commands } 
```

## <a name="span-idddktokenelsifdbgspanspan-idddktokenelsifdbgspansyntax-elements"></a><span id="ddk_token_elsif_dbg"></span><span id="DDK_TOKEN_ELSIF_DBG"></span>语法元素


<span id="_______Condition______"></span><span id="_______condition______"></span><span id="_______CONDITION______"></span> *Condition*   
指定的条件。 如果此计算结果为零，则将其视为 false;否则为 true。 封闭*条件*在括号是可选的。 *条件*必须是一个表达式，而不是调试器命令。 默认表达式计算器将评估 (MASM 或C++)。 有关详细信息，请参阅[数值表达式语法](numerical-expression-syntax.md)。

<span id="_______Commands______"></span><span id="_______commands______"></span><span id="_______COMMANDS______"></span> *命令*   
指定一个或多个命令将有条件地执行。 下面的命令块必须括在大括号，即使它包含单个命令。 之前的右大括号不需要后接分号，应由分号，但最后一个命令分隔的多个命令。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关其他控制流令牌在调试器命令程序及其用法的信息，请参阅[使用调试器命令程序](using-debugger-command-programs.md)。

 

 





