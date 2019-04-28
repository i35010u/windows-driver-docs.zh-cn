---
title: .kill（终止进程）
description: 在用户模式下，.kill 命令结束正在调试的进程。
ms.assetid: e4bc13e4-2566-4438-9ae7-a5ba05b727de
keywords:
- .kill （终止进程） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .kill (Kill Process)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a3940664ca0131d87aa42b23ffd6e99fca9c6d36
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336334"
---
# <a name="kill-kill-process"></a>.kill（终止进程）


在用户模式下 **.kill**命令将结束正在调试的进程。

在内核模式下 **.kill**命令将结束目标计算机上的进程。

用户模式语法

```dbgcmd
.kill [ /h | /n ]
```

内核模式语法

```dbgcmd
.kill Process 
```

## <a name="span-idddkmetakillprocessdbgspanspan-idddkmetakillprocessdbgspanparameters"></a><span id="ddk_meta_kill_process_dbg"></span><span id="DDK_META_KILL_PROCESS_DBG"></span>参数


<span id="________h______"></span><span id="________H______"></span> **/h**   
（仅限用户模式）将继续并标记为已处理的任何未完成的调试事件。 这是默认设置。

<span id="________n______"></span><span id="________N______"></span> **/n**   
（仅限用户模式）任何未完成的调试事件将可继续运行而无需被标记为已处理。

<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span> *Process*   
指定要终止的进程的地址。 如果*进程*省略或零，默认过程有关的当前系统状态将被终止。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

在内核模式下，在 Microsoft Windows Server 2003 和更高版本的 Windows 上支持此命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
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

在用户模式下，此命令将结束正在调试的进程。 如果调试器已附加到子进程，则可以使用 **.kill**结束但不结束父进程的子进程。 有关详细信息，请参阅示例。

在内核模式下，此命令计划终止在目标计算机上所选的进程。 目标可以运行下一次 (例如，通过使用[ **g （转向）** ](g--go-.md)命令)，指定的进程已结束。

不能在局部内核调试期间使用此命令。

<a name="examples"></a>示例
--------

**使用.childdbg**

假设您需要将调试器附加到父进程 (Parent.exe) 之前创建的子进程。 可以输入命令[ **.childdbg 1** ](-childdbg--debug-child-processes-.md)通知调试器附加到父创建任何子进程。

```dbgcmd
1:001> .childdbg 1
Processes created by the current process will be debugged
```

现在，让父进程运行，并在之后它已创建子进程发生中断。 使用[ **|（进程状态）** ](---process-status-.md)命令以查看允许的父和子进程的进程数。

```dbgcmd
0:002> |*
.  0    id: 7f8 attach  name: C:\Parent\x64\Debug\Parent.exe
   1    id: 2d4 child   name: notepad.exe
```

在上面的输出中的子进程 (notepad.exe) 数为 1。 在第一行的开始处的点 （.） 告诉我们，父进程是当前的过程。 若要使子元素的进程当前进程，请输入 **| 1 s**。

```dbgcmd
0:002> |1s
...
1:001> |*
#  0    id: 7f8 attach  name: C:\Parent\x64\Debug\Parent.exe
.  1    id: 2d4 child   name: notepad.exe
```

若要终止子进程，输入命令 **.kill**。 父进程继续运行。

```dbgcmd
1:001> .kill
Terminated.  Exit thread and process events will occur.
1:001> g
```

**使用-o 参数**

当您启动的 WinDbg 或 CDB 时，可以使用 **-o**参数，以让调试程序应附加到子进程。 例如，以下命令启动的 WinDbg 中，这将启动并将附加到 Parent.exe。 当 Parent.exe 创建子进程时，WinDbg 将附加到子进程。

**windbg -g -G -o Parent.exe**

有关详细信息，请参阅[ **WinDbg 命令行选项**](windbg-command-line-options.md)并[ **CDB 命令行选项**](cdb-command-line-options.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>版本:(Kernel mode) 支持在 Windows Server 2003 及更高版本。</p></td>
</tr>
</tbody>
</table>

 

 





