---
title: for_each_process
description: For_each_process 扩展为目标中的每个进程执行指定的调试器命令。
keywords:
- for_each_process Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- for_each_process
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9f1a219f83b8c4db47b1425dbfe755bebebfbdd8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815507"
---
# <a name="for_each_process"></a>！对于 \_ 每个 \_ 进程


**对于 \_ 每个 \_ 进程** 扩展，将为目标中的每个进程执行指定的调试器命令。

```dbgcmd
!for_each_process ["CommandString"] 
!for_each_process -? 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span>*Command.commandstring*   
指定要为每个进程执行的调试器命令。

如果 *command.commandstring* 包含多个命令，请用分号分隔它们 (; ) 并将 *command.commandstring* 括在引号中 ( ") 。 如果 *command.commandstring* 括在引号中，则 *command.commandstring* 中的各个命令不能包含引号。 在 *command.commandstring* 中， **@ \# 进程** 将替换为进程地址。

<span id="_______-_______"></span> **-?**   
在调试器中显示此扩展的帮助命令窗口。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

此扩展仅适用于内核模式，即使它驻留在 Ext.dll 中。

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

有关进程的常规信息，请参阅 [线程和进程](controlling-threads-and-processes.md)。 有关操作或获取有关进程的信息的信息，请参阅 [控制进程和线程](controlling-processes-and-threads.md)。

<a name="remarks"></a>备注
-------

如果未提供任何参数，则调试器将显示所有进程的列表以及时间和优先级统计信息。 这等效于输入 [**！ process @ \# process 0**](-process.md) 作为 *command.commandstring* 值。

若要在任何时候终止执行，请在 KD) 中按) 的 CTRL + BREAK (，并按 CTRL + C (。

 

 





