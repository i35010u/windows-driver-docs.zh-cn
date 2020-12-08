---
title: ~s（设置当前线程）
description: ~ S 命令将设置或显示当前线程号。
keywords:
- ~ s (设置当前线程) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ~s (Set Current Thread)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: abf181b70b12a1d9a05b4e470edb4b741e8e1509
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805789"
---
# <a name="s-set-current-thread"></a>~s（设置当前线程）


**~ S** 命令将设置或显示当前线程号。

在用户模式下， **~ s** 用于设置当前线程。 不要将此命令与 [**~ s (Change Current Processor)**](-s--change-current-processor-.md) 命令混淆， (仅适用于内核模式) ， [**| s (设置当前进程)**](-s--set-current-process-.md) command， [**| |s (设置当前系统)**](--s--set-current-system-.md) 命令或 [**s (Search Memory)**](s--search-memory-.md) 命令。

```dbgcmd
~Thread s 
~ s 
```

## <a name="span-idddk_cmd_set_current_thread_dbgspanspan-idddk_cmd_set_current_thread_dbgspanparameters"></a><span id="ddk_cmd_set_current_thread_dbg"></span><span id="DDK_CMD_SET_CURRENT_THREAD_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*Thread*   
指定要设置或显示的线程。 有关语法的详细信息，请参阅 [线程语法](thread-syntax.md)。

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

只能在用户模式下指定线程。 在内核模式下，颚化 (~) 引用处理器。

如果使用 **~ s** 语法，则调试器会显示有关当前线程的信息。

此命令还将反汇编当前系统、进程和线程的当前指令。

 

 





