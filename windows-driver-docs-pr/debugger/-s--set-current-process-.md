---
title: 's (设置当前进程) '
description: S 命令设置或显示当前进程号。
keywords:
- s (设置当前进程) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- s (Set Current Process)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c0089c91f74c46de18e39b2be8cb771f85a80307
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805827"
---
# <a name="s-set-current-process"></a>|s（设置当前进程）


**| S** 命令将设置或显示当前进程号。

不要将此命令与 [**(搜索内存)**](s--search-memory-.md)、 [**~ s (更改当前处理器)**](-s--change-current-processor-.md)、 [**~ s (设置为当前线程)**](-s--set-current-thread-.md)或 [**| |s (设置当前系统)**](--s--set-current-system-.md) 命令。

```dbgcmd
|Process s 
| s 
```

## <a name="span-idddk_cmd_set_current_process_dbgspanspan-idddk_cmd_set_current_process_dbgspanparameters"></a><span id="ddk_cmd_set_current_process_dbg"></span><span id="DDK_CMD_SET_CURRENT_PROCESS_DBG"></span>参数


<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span>*处理*   
指定要设置或显示的进程。 有关语法的详细信息，请参阅 [处理语法](process-syntax.md)。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关显示或控制进程和线程的其他方法的详细信息，请参阅 [控制进程和线程](controlling-processes-and-threads.md)。

<a name="remarks"></a>备注
-------

只能在用户模式下指定进程。

如果使用 **| s** 语法，则调试器会显示有关当前进程的信息。

此命令还将反汇编当前系统、进程和线程的当前指令。

 

 





