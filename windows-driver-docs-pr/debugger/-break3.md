---
title: .break
description: .Break 令牌的行为类似于在 C 中 break 关键字
ms.assetid: 577e74d1-824f-424a-b30e-a82fe2d682f1
keywords:
- .break Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .break
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dc0db0a953def999e02f40bfb1674503ecc33a1a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334668"
---
# <a name="break"></a>.break


**.Break**令牌的行为类似于**中断**在 C 中的关键字

```dbgcmd
 .for (...) { ... ; .if (Condition) .break ; ...} 

.while (...) { ... ; .if (Condition) .break ; ...} 

.do { ... ; .if (Condition) .break ; ...} (...) 
```

## <span id="ddk_token_break_dbg"></span><span id="DDK_TOKEN_BREAK_DBG"></span>


### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关其他控制流令牌在调试器命令程序及其用法的信息，请参阅[使用调试器命令程序](using-debugger-command-programs.md)。

<a name="remarks"></a>备注
-------

**.Break**令牌可在任何[ **。 有关**](-for.md)， [ **.while**](-while.md)，或[ **执行**](-do.md)循环。

由于没有控制流令牌等效于 C **goto**语句中，您通常使用 **.break**令牌内[**如果**](-if.md)条件，如上述语法示例中所示。 但是，这不是实际必需的。

 

 





