---
title: .elsif
description: 在 C 中，elsif 标记的行为类似于 else if 关键字。
keywords:
- 。 elsif Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .elsif
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1679af8a0e9488f35291c5c4439fa4a51778cc83
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792047"
---
# <a name="elsif"></a>.elsif


在 C 中， **elsif** 标记的行为类似于 **else if** 关键字。

```dbgcmd
.if (Condition) { Commands } .elsif (Condition) { Commands } 

.if (Condition) { Commands } .elsif (Condition) { Commands } .else { Commands } 
```

## <a name="span-idddk_token_elsif_dbgspanspan-idddk_token_elsif_dbgspansyntax-elements"></a><span id="ddk_token_elsif_dbg"></span><span id="DDK_TOKEN_ELSIF_DBG"></span>语法元素


<span id="_______Condition______"></span><span id="_______condition______"></span><span id="_______CONDITION______"></span>*条件*   
指定条件。 如果此值为零，则将其视为 false;否则为 true。 括号中的封闭 *条件* 是可选的。 *Condition* 必须是表达式，而不能是调试器命令。 它将通过默认表达式计算器 (MASM 或 c + +) 进行计算。 有关详细信息，请参阅 [数值表达式语法](numerical-expression-syntax.md)。

<span id="_______Commands______"></span><span id="_______commands______"></span><span id="_______COMMANDS______"></span>*命令*   
指定一个或多个将有条件执行的命令。 此命令块需要括在大括号中，即使它包含单个命令也是如此。 应该用分号分隔多个命令，但右大括号前的最后一个命令无需后跟分号。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关其他控制流令牌及其在调试器命令程序中的使用的信息，请参阅 [使用调试器命令程序](using-debugger-command-programs.md)。

 

 





