---
title: ~f（冻结线程）
description: ~ F 命令冻结给定线程，导致其停止并等待，直到它被解冻。请勿将此命令与 f (Fill Memory) 命令混淆。
keywords:
- ~ f (冻结线程) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ~f (Freeze Thread)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fd2f249edf30061464d5d6fbbdfd6eb903dd44f3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799873"
---
# <a name="f-freeze-thread"></a>~f（冻结线程）


**~ F** 命令冻结给定线程，导致其停止并等待，直到它被解冻。

请勿将此命令与 [**f (Fill Memory)**](f--fp--fill-memory-.md) 命令混淆。

```dbgcmd
~Thread f 
```

## <a name="span-idddk_cmd_freeze_thread_dbgspanspan-idddk_cmd_freeze_thread_dbgspanparameters"></a><span id="ddk_cmd_freeze_thread_dbg"></span><span id="DDK_CMD_FREEZE_THREAD_DBG"></span>参数


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*Thread*   
指定要冻结的线程。 有关语法的详细信息，请参阅 [线程语法](thread-syntax.md)。

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

若要详细了解冻结线程的行为方式和控制线程的冻结和挂起的其他命令的列表，请参阅 [控制进程和线程](controlling-processes-and-threads.md)。

<a name="remarks"></a>备注
-------

只能在用户模式下指定线程。 在内核模式下，颚化 (~) 引用处理器。

**~ F** 命令导致指定的线程冻结。 当调试器允许目标应用程序继续执行时，在此线程保持停止状态时，其他线程会按预期方式执行。

下面的示例演示如何使用此命令。 以下命令显示所有线程的当前状态。

```dbgcmd
0:000> ~* k
```

以下命令将冻结导致当前异常的线程。

```dbgcmd
0:000> ~# f
```

以下命令将检查此线程的状态是否为 "已挂起"。

```dbgcmd
0:000> ~* k
```

以下命令 unfreezes 线程号123。

```dbgcmd
0:000> ~123 u
```

 

 





