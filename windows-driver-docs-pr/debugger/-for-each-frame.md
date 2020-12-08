---
title: for_each_frame
description: For_each_frame 扩展对当前线程的堆栈中的每个帧执行一次调试器命令。
keywords:
- for_each_frame Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- for_each_frame
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 44ef224ac416bd7d3ce5553545b26a8f9c49437c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822675"
---
# <a name="for_each_frame"></a>！对于 \_ 每个 \_ 帧


**对于 \_ 每个帧扩展，每个 \_ 帧** 扩展对当前线程堆栈中的每个帧执行一次调试器命令。

```dbgcmd
!for_each_frame ["CommandString"] 
!for_each_frame -?
```

## <a name="span-idddk__for_each_frame_dbgspanspan-idddk__for_each_frame_dbgspanparameters"></a><span id="ddk__for_each_frame_dbg"></span><span id="DDK__FOR_EACH_FRAME_DBG"></span>参数


<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span>*Command.commandstring*   
指定每个帧执行一次的调试器命令。 如果 *command.commandstring* 包含多个命令，则必须用分号分隔它们，并将 *command.commandstring* 括在引号中。 如果包含多个命令，则 *command.commandstring* 中的单个命令不能包含引号。 若要在 *command.commandstring* 中引用当前帧的索引，请使用 @ $frame pseudoregister。

<span id="_______-_______"></span> **-?**   
在 [调试器命令窗口](debugger-command-window.md)中显示此扩展的一些帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关本地上下文的详细信息，请参阅 [更改上下文](changing-contexts.md)。

<a name="remarks"></a>备注
-------

如果未指定任何参数，则 **\_ 每个 \_ 帧** 扩展的！将显示所有帧及其帧索引的列表。 有关所有框架的更详细列表，请使用 [**k (显示 Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令。

[**K**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令最多可遍历256帧。 对于每个枚举帧，该帧暂时成为当前的本地上下文 (类似于 [**. 帧 () 命令) 设置本地上下文**](-frame--set-local-context-.md) 。 设置上下文后，会执行 *command.commandstring* 。 使用完所有帧后，本地上下文将重置为你在 **为 \_ 每个 \_ 帧** 扩展使用！之前的值。

如果包括 *command.commandstring*，则在对该帧执行命令前，调试器将显示该框架及其索引。

以下命令显示当前堆栈的所有局部变量。

```dbgcmd
!for_each_frame !for_each_local dt @#Local
```

 

 





