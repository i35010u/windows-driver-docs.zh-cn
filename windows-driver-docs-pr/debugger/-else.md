---
title: .else
description: .Else 令牌的行为类似于在 C 中的其他关键字
ms.assetid: aa783a66-2b28-40d1-a943-67a26e668612
keywords:
- .else Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .else
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5d82180b5efcbdf4b89252e17a71979be55099f2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541747"
---
# <a name="else"></a>.else


**.Else**令牌的行为类似于**其他**在 C 中的关键字

```dbgcmd
.if (Condition) { Commands } .else { Commands } 

.if (Condition) { Commands } .elsif (Condition) { Commands } .else { Commands } 
```

## <a name="span-idddktokenelsedbgspanspan-idddktokenelsedbgspansyntax-elements"></a><span id="ddk_token_else_dbg"></span><span id="DDK_TOKEN_ELSE_DBG"></span>语法元素


<span id="_______Commands______"></span><span id="_______commands______"></span><span id="_______COMMANDS______"></span> *命令*   
指定一个或多个命令将有条件地执行。 下面的命令块必须括在大括号，即使它包含单个命令。 之前的右大括号不需要后接分号，应由分号，但最后一个命令分隔的多个命令。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关其他控制流令牌在调试器命令程序及其用法的信息，请参阅[使用调试器命令程序](using-debugger-command-programs.md)。

 

 





