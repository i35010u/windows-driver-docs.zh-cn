---
title: '; (命令分隔符) '
description: 分号 (;) 字符用于在一行上分隔多个命令。
keywords:
- ;) Windows 调试 (命令分隔符
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- ; (Command Separator)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c0f35a4326c478f867b3fd69a2572b2c47b88137
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800221"
---
# <a name="-command-separator"></a>; (命令分隔符) 


分号 ( **;** ) 字符用于在一行上分隔多个命令。

```dbgcmd
    Command1 ; Command2 [; Command3 ...] 
```

## <a name="span-idddk_token_command_separator_dbgspanspan-idddk_token_command_separator_dbgspanparameters"></a><span id="ddk_token_command_separator_dbg"></span><span id="DDK_TOKEN_COMMAND_SEPARATOR_DBG"></span>参数


<span id="_______Command1__Command2__..."></span><span id="_______command1__command2__..."></span><span id="_______COMMAND1__COMMAND2__..."></span>*Command1.enabled*， *Command2*，.。。  
要执行的命令。

<a name="remarks"></a>备注
-------

命令按从左至右的顺序执行。 除非另行指定，否则单个行中的所有命令都将引用当前线程。 如果某个命令导致线程执行，则该行上的其余命令将延迟，直到该线程停止调试事件。

少量命令后面不能跟一个分号，因为它们会自动将该行的整个余数作为其参数。 其中包括 [**(设置别名)**](as--as--set-alias-.md)、 [**$ &lt; (运行脚本文件)**](-----------------------a---run-script-file-.md)、 **$ &gt; &lt; (运行脚本文件)**，以及以 [**\* (注释行说明符)**](----comment-line-specifier-.md)标记开头的任何命令。

示例如下。 这会将当前程序执行到源行123，打印 **计数器** 的值，然后恢复执行：

```console
0:000> g `:123`; ? poi(counter); g 
```

 

 





