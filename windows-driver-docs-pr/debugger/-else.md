---
title: .else
description: Else 标记在 C 中的行为类似于 else 关键字。
keywords:
- 。否则，Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .else
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 979945521f8206c5aed7dec194cc30e9edb6b722
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817895"
---
# <a name="else"></a>.else


**Else** 标记在 C 中的行为类似于 **else** 关键字。

```dbgcmd
.if (Condition) { Commands } .else { Commands } 

.if (Condition) { Commands } .elsif (Condition) { Commands } .else { Commands } 
```

## <a name="span-idddk_token_else_dbgspanspan-idddk_token_else_dbgspansyntax-elements"></a><span id="ddk_token_else_dbg"></span><span id="DDK_TOKEN_ELSE_DBG"></span>语法元素


<span id="_______Commands______"></span><span id="_______commands______"></span><span id="_______COMMANDS______"></span>*命令*   
指定一个或多个将有条件执行的命令。 此命令块需要括在大括号中，即使它包含单个命令也是如此。 应该用分号分隔多个命令，但右大括号前的最后一个命令无需后跟分号。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关其他控制流令牌及其在调试器命令程序中的使用的信息，请参阅 [使用调试器命令程序](using-debugger-command-programs.md)。

 

 





