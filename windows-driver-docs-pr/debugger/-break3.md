---
title: .break
description: Break 标记在 C 中的行为类似于 break 关键字。
keywords:
- 。中断 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .break
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f6511327e2466a00e1ccff779d4e9d61f907ed4a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799955"
---
# <a name="break"></a>.break


**Break** 标记在 C 中的行为类似于 **break** 关键字。

```dbgcmd
 .for (...) { ... ; .if (Condition) .break ; ...} 

.while (...) { ... ; .if (Condition) .break ; ...} 

.do { ... ; .if (Condition) .break ; ...} (...) 
```

## <span id="ddk_token_break_dbg"></span><span id="DDK_TOKEN_BREAK_DBG"></span>


### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关其他控制流令牌及其在调试器命令程序中的使用的信息，请参阅 [使用调试器命令程序](using-debugger-command-programs.md)。

<a name="remarks"></a>备注
-------

可以在任何中使用 **break** 标记。 [**用于**](-for.md)、 [**. while**](-while.md)或 [**. do**](-do.md) 循环。

由于没有与 C **goto** 语句等效的控制流标记，因此通常会在中使用 **break** 标记 [**。如有**](-if.md) 条件，如上述语法示例中所示。 但是，这实际上并不是必需的。

 

 





