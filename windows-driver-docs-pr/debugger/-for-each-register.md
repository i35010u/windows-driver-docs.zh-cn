---
title: for_each_register
description: For_each_register 扩展执行的每个注册指定的命令。
ms.assetid: 496DC161-D082-4C83-A6B6-6BBCE932BE76
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
ms.openlocfilehash: 3e3d8e42aa26416006e772ae0e1e83486b306d56
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533803"
---
# <a name="foreachregister"></a>!for\_each\_register


**！ 有关\_每个\_注册**扩展执行的每个注册指定的命令。

```dbgcmd
!for_each_register -c:CommandString
!for_each_register -?
```

## <a name="span-idddkforeachmoduledbgspanspan-idddkforeachmoduledbgspanparameters"></a><span id="ddk__for_each_module_dbg"></span><span id="DDK__FOR_EACH_MODULE_DBG"></span>参数


<span id="_______-c_CommandString______"></span><span id="_______-c_commandstring______"></span><span id="_______-C_COMMANDSTRING______"></span> **-c:**<em>CommandString</em>   
指定要执行的每个注册的命令。 @ 别名\#寄存器名和 @\#RegisterValue 执行命令期间是否有效。

<span id="_______-_______"></span> **-?**   
显示的帮助 **！ 有关\_每个\_注册**扩展。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Ext.dll

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例


此示例列出了每个注册的名称。

```dbgcmd
0:000> !for_each_register -c:.echo @#RegisterName
rax
rcx
rdx
rbx
...
```

此示例执行[ **！ 地址**](-address.md)为每个注册值。

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

别名是调试器扩展的自变量时 (例如， [ **！ 地址**](-address.md))，使用别名解释程序[ **${} （别名解释器）**](-------alias-interpreter-.md)令牌，以便正确地解析别名。

有关如何定义和别名用作快捷方式的输入字符串的详细信息 (包括使用[ **${}**  ](-------alias-interpreter-.md)令牌)，请参阅[使用别名](using-aliases.md).

 

 





