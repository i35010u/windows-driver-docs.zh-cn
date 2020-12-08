---
title: ~n（挂起线程）
description: ~ N 命令挂起指定线程的执行。不要将此命令与 n (设置 Number Base) 命令混淆。
keywords:
- ~ n (挂起线程) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ~n (Suspend Thread)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 119533468db5e5691da23757bc4bdd8640991432
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790097"
---
# <a name="n-suspend-thread"></a>~n（挂起线程）


**~ N** 命令挂起指定线程的执行。

不要将此命令与 [**n (设置 Number Base)**](n--set-number-base-.md) 命令混淆。

```dbgcmd
~Thread n 
```

## <a name="span-idddk_cmd_suspend_thread_dbgspanspan-idddk_cmd_suspend_thread_dbgspanparameters"></a><span id="ddk_cmd_suspend_thread_dbg"></span><span id="DDK_CMD_SUSPEND_THREAD_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*Thread*   
指定要挂起的一个或一些线程。 有关语法的详细信息，请参阅 [线程语法](thread-syntax.md)。

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
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

若要详细了解暂停计数和挂起线程的行为方式，以及控制挂起和冻结线程的其他命令的列表，请参阅 [控制进程和线程](controlling-processes-and-threads.md)。

<a name="remarks"></a>备注
-------

只能在用户模式下指定线程。 在内核模式下，颚化 (~) 引用处理器。

每次使用 **~ n** 命令时，线程的挂起计数都会增加1。

使用此命令时，将显示该线程的开始地址。

 

 





