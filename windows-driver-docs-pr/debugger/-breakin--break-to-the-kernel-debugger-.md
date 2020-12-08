---
title: .breakin（突入内核调试程序）
description: Breakin 命令从用户模式调试切换到内核模式调试。 当你从内核调试器控制用户模式调试器时，此命令特别有用。
keywords:
- breakin (中断内核调试器) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .breakin (Break to the Kernel Debugger)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d4e6ee652e602b149499a01bfa925c174fcf224f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799957"
---
# <a name="breakin-break-to-the-kernel-debugger"></a>.breakin（突入内核调试程序）


**Breakin** 命令从用户模式调试切换到内核模式调试。 当你从内核调试器控制用户模式调试器时，此命令特别有用。

```dbgcmd
    .breakin 
```

## <span id="ddk_meta_break_to_the_kernel_debugger_dbg"></span><span id="DDK_META_BREAK_TO_THE_KERNEL_DEBUGGER_DBG"></span>


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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果内核模式调试是在启动过程中启用的，并且您正在运行用户模式调试器，则可以使用 **breakin** 命令来停止操作系统并将控制转移到内核调试器。

**Breakin** 命令在调试器的进程上下文中导致内核模式中断。 如果附加了内核调试器，它将变为活动状态。 内核调试器的 [进程上下文](changing-contexts.md) 将自动设置为用户模式调试器的进程，而不是用户模式调试器的目标进程。

调试用户模式问题时，此命令主要用于检索有关系统内核状态的信息。 必须先在内核调试器中继续执行，然后用户模式调试会话才能继续。

当你 [从内核调试器控制用户模式调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md) ，并且用户模式调试器提示在内核调试器中可见时，此命令将暂停用户模式调试器并显示内核模式调试提示。

如果系统无法进入内核调试器，会显示一条错误消息。

如果你使用内核调试器在用户空间中设置断点，并且该断点由用户模式调试器而不是内核调试器捕获，则此命令也很有用。 在用户模式调试器中发出此命令会将控制传输到内核调试器。

如果在启用了调试的系统上使用 **breakin** 命令，则该命令将不起作用。

 

 





