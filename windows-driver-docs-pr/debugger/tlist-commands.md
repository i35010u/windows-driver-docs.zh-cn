---
title: TList 命令
description: TList 命令的语法如下所示
ms.assetid: d1527ffe-ea80-4e02-9a32-b6eccddc1c6a
keywords: TList 命令，Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- TList Commands
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 314c932e87b36173a38ffe67c69fa501e3d905bc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364714"
---
# <a name="tlist-commands"></a>TList 命令


TList 命令的语法如下所示：

```dbgcmd
tlist [/p ProcessName | PID | Pattern | /t | /c | /e | /k | /m [Module] | /s | /v
```

## <a name="span-idddktlistcommandsdtoolsspanspan-idddktlistcommandsdtoolsspanparameters"></a><span id="ddk_tlist_commands_dtools"></span><span id="DDK_TLIST_COMMANDS_DTOOLS"></span>参数


<span id="_______tlist______"></span><span id="_______TLIST______"></span> **tlist**   
不使用其他参数，TList 显示所有正在运行的进程、 其进程标识符 (Pid)，并在其中运行它们，窗口的标题如果有的话。

<span id="________p_______ProcessName______"></span><span id="________p_______processname______"></span><span id="________P_______PROCESSNAME______"></span> **/p** *ProcessName*   
显示指定进程的进程标识符 (PID)。

*ProcessName*是进程 （有或没有文件扩展名） 的名称不一种模式。

如果的值*ProcessName*不匹配任何正在运行的进程、 TList 显示-1。 如果匹配多个进程名称，TList 显示仅第一个匹配进程的 PID。

<span id="_______PID______"></span><span id="_______pid______"></span> *PID*   
显示有关指定 PID 的进程的详细的信息。 有关显示的信息，请参阅下面的"备注"部分。 若要查找进程 ID，请键入**tlist**而无需附加参数。

<span id="_______Pattern______"></span><span id="_______pattern______"></span><span id="_______PATTERN______"></span> *Pattern*   
显示其名称或窗口标题与指定的模式匹配的所有进程的详细的信息。 模式可以是完整名称或正则表达式。

<span id="________t______"></span><span id="________T______"></span> **/t**   
显示每个进程显示为的创建它的进程的子项的任务树。

<span id="________c______"></span><span id="________C______"></span> **/c**   
显示启动每个进程的命令行。

<span id="________e______"></span><span id="________E______"></span> **/e**   
显示每个进程的会话标识符。

<span id="________k______"></span><span id="________K______"></span> **/k**   
显示每个进程中处于活动状态的 COM 组件。

<span id="________m_______Module______"></span><span id="________m_______module______"></span><span id="________M_______MODULE______"></span> **/m** *模块*   
列出的任务在其中加载指定的 DLL 或可执行模块。 模块可以是完整的模块名称或模块名称模式。

<span id="________s______"></span><span id="________S______"></span> **/s**   
显示每个进程中处于活动状态的服务。

<span id="________v______"></span><span id="________V______"></span> **/v**   
显示正在运行进程包括的进程 ID、 会话 ID、 窗口标题、 命令行和进程中运行的服务的详细的信息。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

在进程及其详细显示 (**tlist** *PID*或**tlist** *模式*)，TList 显示以下信息。

-   进程 ID，可执行文件名称、 程序的友好名称。

-   当前工作目录 (CWD)。

-   命令行启动进程 （命令行）。

-   当前虚拟地址空间值。

-   线程数。

-   在进程中运行的线程的列表。 对于每个线程，TList 显示线程 ID (TID)，运行该线程的函数、 入口点的地址、 地址 （如果有） 的最后一个报告的错误，以及线程状态。

-   为进程加载的模块的列表。 对于每个模块，TList 显示版本号、 特性、 模块和模块名称的虚拟地址。

使用时 **/e**参数，仅在以下情况下的进程列表中显示的有效会话标识符。 否则，会话标识符为零 (0)。

-   在 Windows 2000 和 Windows Server 2003，至少一个用户必须连接到控制台会话之外的其他会话。

-   在 Windows XP 中，必须启用快速用户切换和多个用户必须连接到非控制台会话。

-   在 Windows Vista 中，其中所有进程默认情况下都都与两个终端服务会话相关联，至少一个用户必须连接到非控制台会话。

 

 





