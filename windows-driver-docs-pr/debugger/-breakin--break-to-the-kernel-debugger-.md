---
title: .breakin（突入内核调试程序）
description: 从用户模式下调试到内核模式调试切换.breakin 命令。 当正在控制用户模式下的调试程序与内核调试程序时，此命令将特别有用。
ms.assetid: f0dab2c2-60f4-4a85-91bd-6379b247ceaf
keywords:
- .breakin （中断添加到内核调试程序） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .breakin (Break to the Kernel Debugger)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ead826fad720ba8e9729b0044cd2db10064a1fe0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336973"
---
# <a name="breakin-break-to-the-kernel-debugger"></a>.breakin（突入内核调试程序）


**.Breakin**命令切换不同的用户模式下调试到内核模式调试。 当正在控制用户模式下的调试程序与内核调试程序时，此命令将特别有用。

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

 

<a name="remarks"></a>备注
-------

如果在启动过程中启用了内核模式调试，并且正在运行用户模式下调试程序，则可以使用 **.breakin**命令按钮以中断操作系统并将控制权转至内核调试程序。

**.Breakin**命令在调试器的进程上下文中，会导致内核模式下中断。 如果连接了内核调试程序，它将处于活动状态。 内核调试器[进程上下文](changing-contexts.md)将自动设置到用户模式下调试程序，不是用户模式下调试器的目标进程的进程。

此命令时，主要调试用户模式下问题需要检索系统的内核状态有关的信息。 恢复执行内核调试程序中的是必需的用户模式下调试会话才能继续。

如果要[控制用户模式下的调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)和用户模式下调试程序提示符中是可见的内核调试程序，此命令将暂停用户模式下调试程序，并使内核模式调试提示显示。

如果系统无法进入内核调试器，显示一条错误消息。

如果您使用内核调试程序在用户空间中设置断点并由用户模式下调试程序而不是内核调试程序捕获该断点，则也可以使用此命令。 发出此命令在用户模式下调试程序会将控件传输到内核调试程序。

如果 **.breakin**而无法启动时启用调试的系统上使用命令时，它不起作用。

 

 





