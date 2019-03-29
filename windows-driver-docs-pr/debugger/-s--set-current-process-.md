---
title: s （当前进程中设置）
description: S 命令设置或显示当前进程数目。
ms.assetid: 6b4d8e00-426c-496b-9c52-c60faeb0c975
keywords:
- s （当前进程中设置） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- s (Set Current Process)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b2fb36aa01a80ba7e779fcf808aa726d5dda4609
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569007"
---
# <a name="s-set-current-process"></a>|s（设置当前进程）


**| S**命令设置或显示当前进程数目。

不要将使用此命令相混淆[ **s （内存搜索）**](s--search-memory-.md)， [ **~ s （更改当前处理器）**](-s--change-current-processor-.md)， [ **~ s （设置当前线程）**](-s--set-current-thread-.md)，或[ **| |s （设置当前系统）** ](--s--set-current-system-.md)命令。

```dbgcmd
|Process s 
| s 
```

## <a name="span-idddkcmdsetcurrentprocessdbgspanspan-idddkcmdsetcurrentprocessdbgspanparameters"></a><span id="ddk_cmd_set_current_process_dbg"></span><span id="DDK_CMD_SET_CURRENT_PROCESS_DBG"></span>参数


<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span> *Process*   
指定要设置或显示的进程。 有关语法的详细信息，请参阅[过程语法](process-syntax.md)。

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

显示或控制进程和线程的其他方法的详细信息，请参阅[控制进程和线程](controlling-processes-and-threads.md)。

<a name="remarks"></a>备注
-------

仅在用户模式下，可以指定进程。

如果您使用 **| s**语法，调试器将显示有关当前进程的信息。

此命令还将分解为当前系统、 进程和线程的当前指令。

 

 





