---
title: .catch
description: .Catch 令牌用于防止程序终止如果发生错误。它不会不等中的 catch 关键字的行为与C++。
ms.assetid: cda195d8-c0b8-4fb2-99a8-e2e8d338482b
keywords:
- .catch Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .catch
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 25eb75dc00c119855f41f58ea0f7f115665e12e6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334641"
---
# <a name="catch"></a>.catch


**.Catch**令牌用于防止程序终止如果发生错误。

它不会不行为类似于**捕获**中的关键字C++。

```dbgsyntax
    Commands ; .catch { Commands } ; Commands 
```

## <span id="ddk_token_catch_dbg"></span><span id="DDK_TOKEN_CATCH_DBG"></span>


### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关其他控制流令牌在调试器命令程序及其用法的信息，请参阅[使用调试器命令程序](using-debugger-command-programs.md)。

<a name="remarks"></a>备注
-------

**.Catch**标记后跟括号包含它的一个或多个命令。

如果在命令 **.catch**块将生成错误、 显示错误消息、 大括号内的所有其余命令将被忽略，和右大括号之后继续使用第一个命令的执行。

如果 **.catch**是未使用，错误将终止整个调试器命令程序。

可以使用[ **.leave** ](-leave.md)要从其退出 **.catch**块。

 

 





