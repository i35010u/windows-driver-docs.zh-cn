---
title: 调试多个目标
description: 调试多个目标
ms.assetid: 93eb6b49-e7a0-4f30-ade8-94019a1adf43
keywords:
- 多个目标
- system
- 系统概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 323836a8d1f357108793f224bc68473ef5eb1d14
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350582"
---
# <a name="debugging-multiple-targets"></a>调试多个目标


## <span id="ddk_debugging_multiple_targets_dbg"></span><span id="DDK_DEBUGGING_MULTIPLE_TARGETS_DBG"></span>


可以调试多个转储文件，也可以在同一时间 live 用户模式应用程序。 每个目标包含一个或多个进程，每个进程包含一个或多个线程。

这些目标也分为*系统*。 系统是组合在一起以便于标识和操作的目标组中。 系统定义，如下所示：

-   每个内核模式或用户模式转储文件是一个单独的系统。

-   在调试实时用户模式应用程序不同的计算机上 (通过使用[进程服务器](process-servers--user-mode-.md)，如 Dbgsrv)，每个应用程序是独立的系统。

-   调试本地计算机上的实时用户模式应用程序时，应用程序合并到单个系统中。

*当前*或*active*系统是当前正在调试的系统。

### <a name="span-idacquiringmultipletargetsspanspan-idacquiringmultipletargetsspanacquiring-multiple-targets"></a><span id="acquiring_multiple_targets"></span><span id="ACQUIRING_MULTIPLE_TARGETS"></span>获取多个目标

以通常的方式获取的第一个目标。

您可以通过使用调试其他实时的用户模式应用程序[ **.attach （附加到进程）** ](-attach--attach-to-process-.md)或[ **.create （创建进程）** ](-create--create-process-.md)命令后, 跟**g （转向）** 命令。

您可以通过使用调试其他转储文件[ **.opendump （打开转储文件）** ](-opendump--open-dump-file-.md)命令后, 跟**g （转向）** 命令。 启动调试器时，还可以打开多个转储文件。 若要打开多个转储文件，包括多个**z**开关在命令中，每个随后进行了不同的文件名称。

即使进程都位于不同的系统上，可以使用前面的命令。 您必须在每个系统上启动的进程服务器，然后使用具有-premote 参数 **.attach**或 **.create**来标识正确的进程服务器。 如果您使用 **.attach**或 **.create**命令再次而无需指定-premote 参数，调试器将附加到，或创建时，当前系统上的进程。

### <a name="span-idmanipulatingsystemsandtargetsspanspan-idmanipulatingsystemsandtargetsspanmanipulating-systems-and-targets"></a><span id="manipulating_systems_and_targets"></span><span id="MANIPULATING_SYSTEMS_AND_TARGETS"></span>操作的系统和目标

调试开始时，当前系统是最新，调试器附加到的那个。 如果发生异常，当前系统切换到系统上发生此异常。

若要关闭一个目标并继续调试其他目标，请使用[ **.kill （终止进程）** ](-kill--kill-process-.md)命令。 可以使用[ **.detach （与进程分离）** ](-detach--detach-from-process-.md)命令或 WinDbg 的[调试 |分离调试对象](debug---detach-debuggee.md)菜单命令。 这些命令将调试器与目标分离，但不对这些目标运行。

若要控制对多个系统进行调试，可以使用以下方法：

-   [ **| |（系统状态）** ](----system-status-.md)命令显示有关一个或多个系统的信息

-   [ **| |s （设置当前系统）** ](--s--set-current-system-.md)命令，您可以选择当前的系统

-   (仅 WinDbg)[进程和线程窗口](processes-and-threads-window.md)启用显示或选择系统、 进程和线程

通过使用这些命令来选择当前的系统，并使用标准命令[选择的当前进程和线程](controlling-processes-and-threads.md)，可以确定的命令的显示内存和寄存器上下文。

但是，您不能将这些进程的执行。 [ **G （转向）** ](g--go-.md)命令始终会导致要一起执行的所有目标。

**请注意**有采用十分复杂，在调试实时目标和转储目标组合在一起，因为每种类型的调试方式不同命令的行为时。 例如，如果您使用**g （转向）** 命令时当前系统是转储文件，调试器开始执行，但不是能中断返回到调试器，因为换行命令无法识别为有效的调试转储文件。


<a name="example"></a>示例
-------

若要在同一时间使用三个转储文件，可以使用 z 选项启动 WinDbg 时加载它们。 

```console
windbg -z c:\notepad.dmp -z c:\paint.dmp -z c:\calc.dmp
```

有关详细信息请参阅[WinDbg 命令行选项](windbg-command-line-options.md)。 此外可以使用[.opendump](-opendump--open-dump-file-.md)并[ **g （转向）** ](g--go-.md)命令，加载更多的转储文件在调试器中的。 

使用[| |（系统状态）](----system-status-.md)命令来确认是否存在的所有三个系统。

```dbgcmd
||0:0:007> ||
.  0 User mini dump: c:\notepad.dmp
   1 User mini dump: C:\paint.dmp
   2 User mini dump: c:\calc.dmp
```

使用[ **g （转向）** ](g--go-.md)命令完成加载的转储文件。 
```dbgcmd
||0:0:007> g

************* Path validation summary **************
Response                         Time (ms)     Location
Deferred                                       srv*
Symbol search path is: srv*
Executable search path is: 
Windows 10 Version 15063 MP (4 procs) Free x64
Product: WinNt, suite: SingleUserTS
15063.0.amd64fre.rs2_release.170317-1834
Machine Name:
Debug session time: Fri Jun  9 15:52:04.000 2017 (UTC - 7:00)
System Uptime: not available
Process Uptime: 0 days 0:03:44.000
...............................................................
This dump file has a breakpoint exception stored in it.
The stored exception information can be accessed via .ecxr.
ntdll!DbgBreakPoint:
00007ff8`aada8d70 cc              int     3
```

然后，使用[| |s （设置当前系统）](--s--set-current-system-.md)命令以设置当前系统 1，然后显示当前的系统。

```dbgcmd
||1:1:017> ||1s
||1:1:017> ||
   0 User mini dump: c:\notepad.dmp
.  1 User mini dump: c:\paint.dmp
   2 User mini dump: c:\calc.dmp
```

可以使用[.detach](-detach--detach-from-process-.md)命令完成后查看当前的转储文件。

```dbgcmd
||1:1:017> .detach
ntdll!DbgBreakPoint:
00007ff8`aada8d70 cc              int     3
Detached
||0:0:007> ||
.  0 User mini dump: c:\notepad.dmp
   2 User mini dump: c:\calc.dmp
```

<a name="resources"></a>资源
---------

有关调试的其他信息请参阅以下资源。

**丛书**

- 高级的 Windows 调试由 Mario Hewardt 和 Daniel Pravat

- 深入了解 Windows 调试：调试和跟踪 Tarik Soulami 通过 Windows 中的策略的实用指南

- Windows 内部结构通过 Pavel Yosifovich、 Alex Ionescu、 E.Mark Russinovich 和 David A.Solomon 

**视频**

碎片整理工具显示 WinDbg 剧集 13 29 [https://channel9.msdn.com/Shows/Defrag-Tools](https://channel9.msdn.com/Shows/Defrag-Tools) 










