---
title: .continue
description: 在 C 中，continue 标记的行为与 continue 关键字相同。
keywords:
- 。继续 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .continue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7f775778d2847b7c40634afbc4ea0a25040ef50c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803343"
---
# <a name="continue"></a>.continue


在 C 中，continue 标记的行为与 **continue** 关键字相同 **。**

```dbgsyntax
.for (...) { ... ; .if (Condition) .continue ; ... } 

.while (...) { ... ; .if (Condition) .continue ; ... } 

.do { ... ; .if (Condition) .continue ; ... } (...) 
```

## <span id="ddk_token_continue_dbg"></span><span id="DDK_TOKEN_CONTINUE_DBG"></span>


### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关其他控制流令牌及其在调试器命令程序中的使用的信息，请参阅 [使用调试器命令程序](using-debugger-command-programs.md)。

<a name="remarks"></a>备注
-------

可在任何中使用 **continue** 标记。 [**用于**](-for.md)、 [**. while**](-while.md)或 [**. do**](-do.md) 循环。

由于没有与 C goto 语句等效的控制流标记，因此通常会在中使用 **continue** 标记。 [**如果**](-if.md) 条件如此，如以上语法示例中所示。 但是，这实际上并不是必需的。

 

 





