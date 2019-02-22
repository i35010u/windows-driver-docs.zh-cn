---
title: for_each_local
description: For_each_local 扩展在当前帧中执行调试程序命令一次为每个本地变量。
ms.assetid: 2b1d65e6-6322-404e-a94b-90a46035fe9e
keywords:
- for_each_local Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- for_each_local
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0272d43871bccc209522d4521113c2f2a1a31791
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519705"
---
# <a name="foreachlocal"></a>！ 有关\_每个\_本地


**！ 有关\_每个\_本地**扩展执行调试器命令一次为每个本地变量中的当前帧。

```dbgcmd
!for_each_local ["CommandString"] 
!for_each_local -? 
```

## <a name="span-idddkforeachlocaldbgspanspan-idddkforeachlocaldbgspanparameters"></a><span id="ddk__for_each_local_dbg"></span><span id="DDK__FOR_EACH_LOCAL_DBG"></span>参数


<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span> *CommandString*   
指定要在当前堆栈帧中执行一次为每个本地变量的调试器命令。 如果*CommandString*包括多个命令，必须使用分号分隔并括起来*CommandString*引号引起来。 如果包含多个命令，对单个命令中*CommandString*不能包含引号引起来。

内*CommandString*，或在任何脚本中的命令*CommandString*执行，则可以使用 **@\#本地**别名。 此别名替换为本地变量的名称。 这种替换之前发生*CommandString*执行和任何其他分析发生之前。 此别名是区分大小写，并且必须添加一个空格前并后，添加一个空格，即使将别名括在括号中。 如果您使用 c + + 表达式语法，则必须引用此别名来作为 **@ @ (@\#本地)**。

此别名对调用的生存期内只是可用 **！ 有关\_每个\_本地**。 不要混淆此别名使用伪寄存器，固定名称的别名或用户命名别名。

<span id="_______-_______"></span> **-?**   
显示此扩展中的一些帮助文本[调试器命令窗口](debugger-command-window.md)。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关如何显示和更改本地变量和其他与内存相关的命令的说明的详细信息，请参阅[读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

如果未指定任何参数， **！ 有关\_每个\_本地**扩展列出本地变量。 有关本地变量的详细信息，请使用[ **dv （显示本地变量）** ](dv--display-local-variables-.md)命令。

如果启用详细调试程序输出，显示内容包括本地变量的总数和调用扩展时，每次时， *CommandString*执行为该变量的本地变量和文本*CommandString*将回显。

 

 





