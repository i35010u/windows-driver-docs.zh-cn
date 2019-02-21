---
title: for_each_thread
description: For_each_thread 扩展执行将在目标中指定的调试器命令一次为每个线程。
ms.assetid: 4ca8e1bd-1a1b-4fef-a2d9-42c26f9b746b
keywords:
- for_each_thread Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- for_each_thread
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 27874f8e518ebe33cd20de0cda693f63b90f3478
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525022"
---
# <a name="foreachthread"></a>!for\_each\_thread


**！ 有关\_每个\_线程**扩展执行将在目标中指定的调试器命令一次为每个线程。

```dbgcmd
!for_each_thread ["CommandString"] 
!for_each_thread -? 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______CommandString______"></span><span id="_______commandstring______"></span><span id="_______COMMANDSTRING______"></span> *CommandString*   
指定要为每个线程执行的调试器命令。 如果*CommandString*包括多个命令，请使用分号 （;） 分隔并将括*CommandString*用引号 （"）。 如果*CommandString*括在引号中的单个命令*CommandString*不能包含引号引起来。 内*CommandString*，  **@\#线程**线程地址将替换为。

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

有关线程的更多常规信息，请参阅[线程和进程](controlling-threads-and-processes.md)。 有关操作或获取有关线程的信息的详细信息，请参阅[控制进程和线程](controlling-processes-and-threads.md)。

<a name="remarks"></a>备注
-------

如果未不提供任何参数，则调试器将显示所有线程的列表，以及线程等待状态。 这相当于输入[ **！ 线程\#线程 2** ](-process.md)作为*CommandString*值。

可以通过按 CTRL + BREAK （在 WinDbg) 或 CTRL + C （中 KD) 终止的任何点处的执行。

 

 





