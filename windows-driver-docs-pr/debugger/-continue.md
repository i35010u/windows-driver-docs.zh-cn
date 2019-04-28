---
title: .continue
description: .Continue 令牌的行为类似于在 C 中 continue 关键字
ms.assetid: c8f6c69c-d912-4ce4-a9c2-d82c349484a9
keywords:
- .continue Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .continue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e087d011f7978d935b7ba9dfb8a7450dff71610e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334626"
---
# <a name="continue"></a>.continue


**.Continue**令牌的行为类似于**继续**在 C 中的关键字

```dbgsyntax
.for (...) { ... ; .if (Condition) .continue ; ... } 

.while (...) { ... ; .if (Condition) .continue ; ... } 

.do { ... ; .if (Condition) .continue ; ... } (...) 
```

## <span id="ddk_token_continue_dbg"></span><span id="DDK_TOKEN_CONTINUE_DBG"></span>


### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关其他控制流令牌在调试器命令程序及其用法的信息，请参阅[使用调试器命令程序](using-debugger-command-programs.md)。

<a name="remarks"></a>备注
-------

**.Continue**令牌可在任何[ **。 有关**](-for.md)， [ **.while**](-while.md)，或[**执行**](-do.md)循环。

由于没有任何控制流令牌等效于 C goto 语句，您通常将使用 **.continue**令牌内[**如果**](-if.md)条件，如语法中所示上面的示例。 但是，这不是实际必需的。

 

 





