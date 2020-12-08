---
title: for_each_register
description: For_each_register 扩展对每个注册执行指定的命令。
keywords:
- for_each_register Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- for_each_register
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2116c997c430183838248a9629a8f29cc7c59458
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817581"
---
# <a name="for_each_register"></a>！对于 \_ 每个 \_ 寄存器


**适用于 \_ 每个 \_ 注册扩展的！为** 每个寄存器执行指定的命令。

```dbgcmd
!for_each_register -c:CommandString
!for_each_register -?
```

## <a name="span-idddk__for_each_module_dbgspanspan-idddk__for_each_module_dbgspanparameters"></a><span id="ddk__for_each_module_dbg"></span><span id="DDK__FOR_EACH_MODULE_DBG"></span>参数


<span id="_______-c_CommandString______"></span><span id="_______-c_commandstring______"></span><span id="_______-C_COMMANDSTRING______"></span>**-c：**<em>command.commandstring</em>   
指定要为每个寄存器执行的命令。 别名 @ \# 寄存器名和 @ \# RegisterValue 在执行命令期间有效。

<span id="_______-_______"></span> **-?**   
**为 \_ 每个 \_ 寄存器** 扩展显示！的帮助。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Ext.dll

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例


此示例列出了每个寄存器的名称。

```dbgcmd
0:000> !for_each_register -c:.echo @#RegisterName
rax
rcx
rdx
rbx
...
```

此示例对每个 register 值执行 [**！ address**](-address.md) 。

```dbgcmd
0:000> !for_each_register -c:!address ${@#RegisterValue}
...
Usage:                  Stack
Base Address:           00000008`a568f000
End Address:            00000008`a56a0000
Region Size:            00000000`00011000
State:                  00001000    MEM_COMMIT
Protect:                00000004    PAGE_READWRITE
Type:                   00020000    MEM_PRIVATE
Allocation Base:        00000008`a5620000
Allocation Protect:     00000004    PAGE_READWRITE
More info:              ~0k
...
```

<a name="remarks"></a>备注
-------

如果别名是调试器扩展的参数 (例如， [**！ address**](-address.md)) ，请使用别名解释器 [**$ {} (别名解释器)**](-------alias-interpreter-.md) 标记，以便正确解析别名。

有关如何定义和使用别名作为输入字符串的快捷方式的详细信息 (包括使用 [**{} $**](-------alias-interpreter-.md) token) 的详细信息，请参阅 [使用别名](using-aliases.md)。

 

 





