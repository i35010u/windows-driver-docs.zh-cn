---
title: for_each_process
description: For_each_process 扩展的目标中执行一次用于每个进程的指定的调试器命令。
ms.assetid: 28cc0982-43a4-41ba-a26f-6910cc1b77b8
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
ms.openlocfilehash: 593fe189f633221301386a25b8fa5987d542c008
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542790"
---
# <a name="foreachprocess"></a>!for\_each\_process


**！ 有关\_每个\_进程**扩展的目标中执行一次用于每个进程的指定的调试器命令。

```dbgcmd
!for_each_process ["CommandString"] 
!for_each_process -? 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span> *CommandString*   
指定要执行的每个进程的调试器命令。

如果*CommandString*包括多个命令，请使用分号 （;） 分隔并将括*CommandString*用引号 （"）。 如果*CommandString*括在引号中的单个命令*CommandString*不能包含引号引起来。 内*CommandString*，  **@\#过程**由进程地址替换。

<span id="_______-_______"></span> **-?**   
显示此扩展在调试器命令窗口中的帮助。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

此扩展仅在内核模式下，有效，即使它驻留在 Ext.dll 也是如此。

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

有关进程的常规信息，请参阅[线程和进程](controlling-threads-and-processes.md)。 有关操作或获取进程信息的信息，请参阅[控制进程和线程](controlling-processes-and-threads.md)。

<a name="remarks"></a>备注
-------

如果未不提供任何参数，调试器会显示所有进程，以及时间和优先级的统计信息的列表。 这相当于输入[ **！ @ 进程\#进程 0** ](-process.md)作为*CommandString*值。

若要终止执行任何时候，按 CTRL + BREAK （在 WinDbg) 或 CTRL + C （中 KD)。

 

 





