---
title: ;（命令分隔符）
description: 分号 （;） 字符用于分隔多个命令在单个行上的。
ms.assetid: efa59a34-1d1d-4df4-bbb9-b8066c6f3b3c
keywords:
- ;（命令分隔符）Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- ; (Command Separator)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6b23f6eda8fb784bdd47231e454ae124c3e3039e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576714"
---
# <a name="-command-separator"></a>;（命令分隔符）


以分号 ( **;** ) 字符用于分隔多个命令在单个行上的。

```dbgcmd
    Command1 ; Command2 [; Command3 ...] 
```

## <a name="span-idddktokencommandseparatordbgspanspan-idddktokencommandseparatordbgspanparameters"></a><span id="ddk_token_command_separator_dbg"></span><span id="DDK_TOKEN_COMMAND_SEPARATOR_DBG"></span>参数


<span id="_______Command1__Command2__..."></span><span id="_______command1__command2__..."></span><span id="_______COMMAND1__COMMAND2__..."></span> *Command1*， *Command2*，...  
要执行的命令。

<a name="remarks"></a>备注
-------

命令执行按顺序从左到右。 在单个行上的所有命令是都指当前线程，除非另行指定。 如果命令导致要执行的线程，直到该线程停止调试事件，剩余的命令行上将被延迟。

少量的命令不能跟分号，因为它们将自动采用作为其参数的行的整个剩余部分。 其中包括[ **（设置别名） 作为**](as--as--set-alias-.md)， [  **$ &lt; （运行脚本文件）**](-----------------------a---run-script-file-.md)，  **$ &gt; &lt; （运行脚本文件）**，并使用任何命令开头[  **\* （注释行说明符）** ](----comment-line-specifier-.md)令牌。

下面是一个示例。 这执行源行 123 到当前程序时，将的值打印**计数器**，然后继续执行：

```console
0:000> g `:123`; ? poi(counter); g 
```

 

 





