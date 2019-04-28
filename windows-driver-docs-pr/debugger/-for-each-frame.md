---
title: for_each_frame
description: For_each_frame 扩展在当前线程的堆栈中执行调试程序命令一次每个帧。
ms.assetid: 7294dc5e-190f-486f-9079-1fb28d6d484b
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
ms.openlocfilehash: dbf39c37a8a8ecd090f5afd111f9f1980c1c116d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336662"
---
# <a name="foreachframe"></a>!for\_each\_frame


**！ 有关\_每个\_帧**扩展调试器命令一次每个帧中执行当前线程的堆栈。

```dbgcmd
!for_each_frame ["CommandString"] 
!for_each_frame -?
```

## <a name="span-idddkforeachframedbgspanspan-idddkforeachframedbgspanparameters"></a><span id="ddk__for_each_frame_dbg"></span><span id="DDK__FOR_EACH_FRAME_DBG"></span>参数


<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span> *CommandString*   
指定要为每个帧执行一次的调试器命令。 如果*CommandString*包括多个命令，必须使用分号分隔并括起来*CommandString*引号引起来。 如果包含多个命令，对单个命令中*CommandString*不能包含引号引起来。 如果你想要参考中的当前帧的索引*CommandString*，使用 @$ 帧 pseudoregister。

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

有关本地上下文的详细信息，请参阅[更改上下文](changing-contexts.md)。

<a name="remarks"></a>备注
-------

如果未指定任何参数， **！ 有关\_每个\_帧**扩展显示的所有帧和其帧索引列表。 对于所有帧的更详细的列表，请使用[ **k （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令。

[ **K** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令将引导最多 256 个帧。 对于每个枚举的框架，该帧暂时将成为当前的本地上下文 (类似于[ **.frame （设置本地上下文）** ](-frame--set-local-context-.md)命令)。 设置的上下文后， *CommandString*执行。 已使用所有帧后，本地上下文重置为你之前的值都使用 **！ 有关\_每个\_帧**扩展。

如果包括*CommandString*，调试器将显示在帧和该框架执行的命令之前其索引。

下面的命令显示当前堆栈的所有局部变量。

```dbgcmd
!for_each_frame !for_each_local dt @#Local
```

 

 





