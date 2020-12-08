---
title: .kill（终止进程）
description: 在用户模式下，kill 命令结束正在调试的进程。
keywords:
- kill (终止进程) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .kill (Kill Process)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 485a1bbf5e98d5fd0847d75749c160edddec5867
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826751"
---
# <a name="kill-kill-process"></a>.kill（终止进程）


在用户模式下， **kill** 命令结束正在调试的进程。

在内核模式下， **kill** 命令结束目标计算机上的进程。

User-Mode 语法

```dbgcmd
.kill [ /h | /n ]
```

Kernel-Mode 语法

```dbgcmd
.kill Process 
```

## <a name="span-idddk_meta_kill_process_dbgspanspan-idddk_meta_kill_process_dbgspanparameters"></a><span id="ddk_meta_kill_process_dbg"></span><span id="DDK_META_KILL_PROCESS_DBG"></span>参数


<span id="________h______"></span><span id="________H______"></span>**/h**   
 (用户模式仅) 任何未完成的调试事件都将继续并标记为已处理。 这是默认值。

<span id="________n______"></span><span id="________N______"></span>**/n**   
 (用户模式仅) 任何未完成的调试事件都将继续，而不会标记为已处理。

<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span>*处理*   
指定要终止的进程的地址。 如果 *省略或为零* ，则将终止当前系统状态的默认进程。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

在内核模式下，此命令在 Microsoft Windows Server 2003 和更高版本的 Windows 上受支持。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
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

在用户模式下，此命令结束正在调试的进程。 如果调试器附加到子进程，则可以使用 **kill** 来结束子进程，而无需终止父进程。 有关详细信息，请参阅示例。

在内核模式下，此命令将在目标计算机上计划所选进程的终止状态。 下一次目标可运行 (例如，通过使用 [**g (中转)**](g--go-.md) 命令) ，将结束指定的进程。

在本地内核调试过程中不能使用此命令。

<a name="examples"></a>示例
--------

**使用. childdbg**

假设在创建子进程之前，将调试器附加到父进程 ( # A0) 。 可以输入 [**childdbg 1**](-childdbg--debug-child-processes-.md) ，告诉调试器附加到父创建的任何子进程。

```dbgcmd
1:001> .childdbg 1
Processes created by the current process will be debugged
```

现在让父进程运行，并在创建子进程后中断。 使用 " [**| (进程状态")**](---process-status-.md) 命令查看父进程和子进程的进程编号。

```dbgcmd
0:002> |*
.  0    id: 7f8 attach  name: C:\Parent\x64\Debug\Parent.exe
   1    id: 2d4 child   name: notepad.exe
```

在上面的输出中，子进程的编号 ( # A0) 为1。  ( 第一行开头的点 ) 告诉我们父进程是当前进程。 若要使子进程成为当前进程，请输入 **| 1**。

```dbgcmd
0:002> |1s
...
1:001> |*
#  0    id: 7f8 attach  name: C:\Parent\x64\Debug\Parent.exe
.  1    id: 2d4 child   name: notepad.exe
```

若要终止子进程，请输入命令 **kill**。 父进程将继续运行。

```dbgcmd
1:001> .kill
Terminated.  Exit thread and process events will occur.
1:001> g
```

**使用-o 参数**

启动 WinDbg 或 CDB 时，可以使用 **-o** 参数告诉调试器它应附加到子进程。 例如，以下命令将启动 WinDbg，这将启动并附加到 Parent.exe。 当 Parent.exe 创建子进程时，WinDbg 会附加到子进程。

**windbg-g-G-o Parent.exe**

有关详细信息，请参阅 [**WinDbg Command-Line 选项**](windbg-command-line-options.md) 和 [**CDB Command-Line 选项**](cdb-command-line-options.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>版本： Windows Server 2003 及更高版本中支持 (内核模式) 。</p></td>
</tr>
</tbody>
</table>

 

 





