---
title: .leave
description: .Leave 令牌用于从.catch 块中退出。
ms.assetid: 82c5cbf7-bccd-4abf-b52a-2db65e0a0c2c
keywords:
- .leave Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .leave
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 69d8cb0cd70f3e5a85da8b9894c74b9aa371c110
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569246"
---
# <a name="leave"></a>.leave


**.Leave**令牌用于退出[ **.catch** ](-catch.md)块。

```dbgcmd
.catch { ... ; .if (Condition) .leave ; ... } 
```

## <span id="ddk_token_leave_dbg"></span><span id="DDK_TOKEN_LEAVE_DBG"></span>


### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关其他控制流令牌在调试器命令程序及其用法的信息，请参阅[使用调试器命令程序](using-debugger-command-programs.md)。

<a name="remarks"></a>备注
-------

当 **.leave**令牌遇到内[ **.catch** ](-catch.md)阻止，请从块中，并执行与第一个命令将继续在程序退出后的右大括号。

由于没有控制流令牌等效于 C **goto**语句中，您通常使用 **.leave**令牌内[**如果**](-if.md)条件，如上述语法示例中所示。 但是，这不是实际必需的。

 

 





