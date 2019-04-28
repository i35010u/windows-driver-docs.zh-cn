---
title: ~s（设置当前线程）
description: ~ S 命令设置或显示当前的线程数。
ms.assetid: 689d578b-8d31-4049-a374-19ae94d452a9
keywords:
- ~ s （设置当前线程） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ~s (Set Current Thread)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 114768f905bef5a601b4883fc72df1160e8ef34c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335762"
---
# <a name="s-set-current-thread"></a>~s（设置当前线程）


**~ S**命令设置或显示当前的线程数。

在用户模式下 **~ s**设置当前线程。 不要混淆此命令相混淆[ **~ s （更改当前处理器）** ](-s--change-current-processor-.md)命令 （仅在内核模式下的工作方式）， [ **| s （设置当前进程）**](-s--set-current-process-.md)命令， [ **| |s （设置当前系统）** ](--s--set-current-system-.md)命令，或[ **s （内存搜索）** ](s--search-memory-.md)命令。

```dbgcmd
~Thread s 
~ s 
```

## <a name="span-idddkcmdsetcurrentthreaddbgspanspan-idddkcmdsetcurrentthreaddbgspanparameters"></a><span id="ddk_cmd_set_current_thread_dbg"></span><span id="DDK_CMD_SET_CURRENT_THREAD_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
指定要设置或显示的线程。 有关语法的详细信息，请参阅[线程语法](thread-syntax.md)。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>仅限用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息和显示或控制进程和线程的其他方法，请参阅[控制进程和线程](controlling-processes-and-threads.md)。

<a name="remarks"></a>备注
-------

仅在用户模式下，可以指定线程。 在内核模式下颚化符 （~） 是指一个处理器。

如果您使用 **~ s**语法，调试器将显示有关当前线程的信息。

此命令还将分解为当前系统、 进程和线程的当前指令。

 

 





