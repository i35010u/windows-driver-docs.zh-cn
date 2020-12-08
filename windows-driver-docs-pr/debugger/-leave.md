---
title: .leave
description: Leave 标记用于退出 catch 块。
keywords:
- 。退出 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .leave
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 79abf12cff86784db0711e8f7f13d45b1a1c43a8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804037"
---
# <a name="leave"></a>.leave


**Leave** 标记用于退出 [**catch**](-catch.md)块。

```dbgcmd
.catch { ... ; .if (Condition) .leave ; ... } 
```

## <span id="ddk_token_leave_dbg"></span><span id="DDK_TOKEN_LEAVE_DBG"></span>


### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关其他控制流令牌及其在调试器命令程序中的使用的信息，请参阅 [使用调试器命令程序](using-debugger-command-programs.md)。

<a name="remarks"></a>备注
-------

当在 [**catch**](-catch.md)块内遇到 **leave** 标记时，程序从块退出，并使用右大括号后面的第一个命令继续执行。

由于不存在与 C **goto** 语句等效的控制流标记，因此通常会在中使用 **. leave** 标记 [**。如果有**](-if.md) 条件，如上述语法示例中所示。 但是，这实际上并不是必需的。

 

 





