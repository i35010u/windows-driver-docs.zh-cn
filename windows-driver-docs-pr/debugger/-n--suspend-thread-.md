---
title: ~ n （挂起线程）
description: ~ N 命令挂起指定的线程的执行。不要混淆此命令使用 n (设置数量 Base) 命令。
ms.assetid: 4b1063ad-edba-4cd3-9084-dc6c08c69f55
keywords:
- ~ n （挂起线程） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ~n (Suspend Thread)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 64c0026bbc37a027ca11865800c1e28e1381f701
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522278"
---
# <a name="n-suspend-thread"></a>~ n （挂起线程）


**~ N**命令挂起指定的线程的执行。

不要将使用此命令相混淆[ **n (设置数量 Base)** ](n--set-number-base-.md)命令。

```dbgcmd
~Thread n 
```

## <a name="span-idddkcmdsuspendthreaddbgspanspan-idddkcmdsuspendthreaddbgspanparameters"></a><span id="ddk_cmd_suspend_thread_dbg"></span><span id="DDK_CMD_SUSPEND_THREAD_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
指定的线程或线程挂起。 有关语法的详细信息，请参阅[线程语法](thread-syntax.md)。

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
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关挂起计数和如何挂起的线程的行为并控制挂起和冻结的线程的其他命令的列表，请参阅[控制进程和线程](controlling-processes-and-threads.md)。

<a name="remarks"></a>备注
-------

仅在用户模式下，可以指定线程。 在内核模式下颚化符 （~） 是指一个处理器。

使用每次 **~ n**命令时，线程的挂起计数增加 1。

使用此命令时，将显示线程的起始地址。

 

 





