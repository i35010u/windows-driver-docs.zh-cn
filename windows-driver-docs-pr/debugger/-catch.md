---
title: .catch
description: 如果发生错误，则使用 catch 标记阻止程序终止。它的行为类似于 c + + 中的 catch 关键字。
keywords:
- 。捕获 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .catch
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 732b2647cbc508e997e7caacbd60cda83ebf4bbd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814089"
---
# <a name="catch"></a>.catch


如果发生错误，则使用 **catch** 标记阻止程序终止。

它的行为类似于 c + + 中的 **catch** 关键字。

```dbgsyntax
    Commands ; .catch { Commands } ; Commands 
```

## <span id="ddk_token_catch_dbg"></span><span id="DDK_TOKEN_CATCH_DBG"></span>


### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关其他控制流令牌及其在调试器命令程序中的使用的信息，请参阅 [使用调试器命令程序](using-debugger-command-programs.md)。

<a name="remarks"></a>备注
-------

**Catch** 标记后跟一个或多个命令的大括号。

如果 **catch** 块中的命令生成错误，则会显示错误消息，将忽略大括号内的所有剩余命令，并使用右大括号后面的第一个命令继续执行。

如果未使用 **catch** ，则错误将终止整个调试器命令程序。

你可以使用 [**。**](-leave.md) 请退出以退出 **catch** 块。

 

 





