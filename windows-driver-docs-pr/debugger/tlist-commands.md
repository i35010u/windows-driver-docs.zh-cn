---
title: TList 命令
description: Tlist.exe 命令的语法如下所示
keywords: Tlist.exe 命令，Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- TList Commands
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0648a63d6061dfa83115aa431d15ec3e1b34de48
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839319"
---
# <a name="tlist-commands"></a>TList 命令


Tlist.exe 命令的语法如下所示：

```dbgcmd
tlist [/p ProcessName | PID | Pattern | /t | /c | /e | /k | /m [Module] | /s | /v
```

## <a name="span-idddk_tlist_commands_dtoolsspanspan-idddk_tlist_commands_dtoolsspanparameters"></a><span id="ddk_tlist_commands_dtools"></span><span id="DDK_TLIST_COMMANDS_DTOOLS"></span>参数


<span id="_______tlist______"></span><span id="_______TLIST______"></span>**tlist.exe**   
如果没有其他参数，Tlist.exe 会显示所有正在运行的进程、其进程标识符 (Pid) ，以及运行它们的窗口的标题（如果有）。

<span id="________p_______ProcessName______"></span><span id="________p_______processname______"></span><span id="________P_______PROCESSNAME______"></span>**/P** *ProcessName*   
显示指定进程 (PID) 的进程标识符。

*ProcessName* 是带有或不带文件扩展名的进程 (名称) ，而不是模式。

如果 *ProcessName* 的值与任何正在运行的进程都不匹配，则 tlist.exe 将显示-1。 如果它与多个进程名称匹配，则 Tlist.exe 仅显示第一个匹配进程的 PID。

<span id="_______PID______"></span><span id="_______pid______"></span>*PID*   
显示有关 PID 指定的进程的详细信息。 有关显示的信息，请参阅下面的 "备注" 部分。 若要查找进程 ID，请键入 **tlist.exe** 而不使用其他参数。

<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span>*模式*   
显示其名称或窗口标题与指定模式匹配的所有进程的详细信息。 Pattern 可以是完整名称，也可以是正则表达式。

<span id="________t______"></span><span id="________T______"></span>**/t**   
显示一个任务树，其中每个进程显示为创建该进程的进程的子进程。

<span id="________c______"></span><span id="________C______"></span>**/c**   
显示启动每个进程的命令行。

<span id="________e______"></span><span id="________E______"></span>**/e**   
显示每个进程的会话标识符。

<span id="________k______"></span><span id="________K______"></span>**/k**   
显示每个进程中处于活动状态的 COM 组件。

<span id="________m_______Module______"></span><span id="________m_______module______"></span><span id="________M_______MODULE______"></span>**/M** *模块*   
列出在其中加载指定 DLL 或可执行模块的任务。 模块可以是完整的模块名称或模块名称模式。

<span id="________s______"></span><span id="________S______"></span>**/s**   
显示每个进程中处于活动状态的服务。

<span id="________v______"></span><span id="________V______"></span>**/v**   
显示正在运行的进程的详细信息，包括进程 ID、会话 ID、窗口标题、命令行和进程中运行的服务。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

在详细显示进程 (**Tlist.exe** *PID* 或 **Tlist.exe** *模式*) 中，tlist.exe 将显示以下信息。

-   进程 ID、可执行文件名称、程序的友好名称。

-   当前工作目录 (CWD) 。

-   启动进程的命令行 (CmdLine) 。

-   当前虚拟地址空间值。

-   线程数。

-   进程中运行的线程的列表。 对于每个线程，Tlist.exe 将显示线程 ID (TID) 、线程正在运行的函数、入口点的地址、上次报告的错误的地址 (if 任何) 和线程状态。

-   为进程加载的模块的列表。 对于每个模块，Tlist.exe 将显示模块的版本号、属性、虚拟地址和模块名称。

使用 **/e** 参数时，有效会话标识符仅出现在以下条件下的 "进程" 列表中。 否则，会话标识符为零 (0) 。

-   在 Windows XP 上，必须启用快速用户切换，并且多个用户必须连接到非控制台会话。

-   在 Windows Vista 上，在默认情况下，所有进程都与两个终端服务会话关联，必须至少有一个用户连接到非控制台会话。
