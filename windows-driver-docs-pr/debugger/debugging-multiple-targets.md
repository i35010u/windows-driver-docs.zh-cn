---
title: 调试多个目标
description: 调试多个目标
keywords:
- 多个目标
- system
- 系统，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ead361b12a25dfdb1a2340db56922968a43d3c0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817523"
---
# <a name="debugging-multiple-targets"></a>调试多个目标


## <span id="ddk_debugging_multiple_targets_dbg"></span><span id="DDK_DEBUGGING_MULTIPLE_TARGETS_DBG"></span>


可以同时调试多个转储文件或实时用户模式应用程序。 每个目标都包含一个或多个进程，每个进程都包含一个或多个线程。

这些目标还会组合到 *系统* 中。 系统是分组在一起以方便标识和操作的一组目标。 系统定义如下：

-   每个内核模式或用户模式转储文件都是单独的系统。

-   如果要在不同计算机上调试实时用户模式应用程序 (使用 [进程服务器](process-servers--user-mode-.md)（如 Dbgsrv) ），则每个应用程序都是一个单独的系统。

-   当你在本地计算机上调试实时用户模式应用程序时，应用程序将合并到一个系统中。

*当前* 或 *活动* 系统是当前正在调试的系统。

### <a name="span-idacquiring_multiple_targetsspanspan-idacquiring_multiple_targetsspanacquiring-multiple-targets"></a><span id="acquiring_multiple_targets"></span><span id="ACQUIRING_MULTIPLE_TARGETS"></span>获取多个目标

首先以常规方式获取第一个目标。

你可以通过使用 [**. attach (附加到进程)**](-attach--attach-to-process-.md) 或 [**创建 (创建进程)**](-create--create-process-.md) 命令，然后使用 **g (中转)** 命令调试其他实时用户模式应用程序。

可以使用 [**. opendump (打开转储文件)**](-opendump--open-dump-file-.md) 命令调试其他转储文件，后跟 **g (中转)** 命令。 启动调试器时，还可以打开多个转储文件。 若要打开多个转储文件，请在命令中包含多个 **z** 开关，每个开关后跟不同的文件名。

即使进程在不同的系统上，也可以使用上述命令。 必须在每个系统上启动进程服务器，并将-premote 参数与 **. attach** 或 **. create** 一起使用来标识正确的进程服务器。 如果在未指定-premote 参数的情况下再次使用 " **attach** " 或 " **create** " 命令，调试器将在当前系统上附加或创建进程。

### <a name="span-idmanipulating_systems_and_targetsspanspan-idmanipulating_systems_and_targetsspanmanipulating-systems-and-targets"></a><span id="manipulating_systems_and_targets"></span><span id="MANIPULATING_SYSTEMS_AND_TARGETS"></span>操作系统和目标

调试开始时，当前系统是调试器最近附加到的系统。 如果发生异常，则当前系统会切换到发生此异常的系统。

若要关闭一个目标并继续调试其他目标，请使用 [**kill (Kill 进程)**](-kill--kill-process-.md) 命令。 您可以使用 [**(从进程中分离)**](-detach--detach-from-process-.md) 命令或 WinDbg 的 [调试 |改为分离调试对象](debug---detach-debuggee.md) 菜单命令。 这些命令将调试器与目标分离，但使目标保持运行状态。

若要控制多个系统的调试，可以使用以下方法：

-   [**| | (系统状态)**](----system-status-.md)命令显示有关一个或多个系统的信息

-   [**| |s (设置当前系统)**](--s--set-current-system-.md)命令使您可以选择当前系统

-   仅 (WinDbg) " [进程和线程" 窗口](processes-and-threads-window.md) 可让你显示或选择系统、进程和线程

通过使用这些命令选择当前系统，并通过使用标准命令 [选择当前进程和线程](controlling-processes-and-threads.md)，你可以确定显示内存和注册的命令的上下文。

但是，不能分离这些进程的执行。 [**G (中转)**](g--go-.md)命令始终导致所有目标一起执行。

**注意**   在调试实时目标并将目标转储到一起时，有一些复杂的问题，因为每种调试类型的命令的行为有所不同。 例如，如果在当前系统为转储文件时使用 **g (中转)** 命令，则调试器将开始执行，但无法中断到调试器中，因为 break 命令未被识别为对转储文件调试无效。


<a name="example"></a>示例
-------

若要同时使用三个转储文件，可以使用-z 选项在 WinDbg 开始时加载它们。 

```console
windbg -z c:\notepad.dmp -z c:\paint.dmp -z c:\calc.dmp
```

有关详细信息，请参阅 [WinDbg Command-Line 选项](windbg-command-line-options.md)。 你还可以使用 [opendump](-opendump--open-dump-file-.md)  和 [**g (中转)**](g--go-.md) 命令在调试器中加载其他转储文件。 

使用  [| | (系统状态) ](----system-status-.md) 命令确认所有三个系统都存在。

```dbgcmd
||0:0:007> ||
.  0 User mini dump: c:\notepad.dmp
   1 User mini dump: C:\paint.dmp
   2 User mini dump: c:\calc.dmp
```

使用 [**g (中转)**](g--go-.md) 命令完成转储文件的加载。 
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

然后使用  [| |s (设置当前系统) ](--s--set-current-system-.md) 命令，将当前系统设置为系统1，然后显示当前系统。

```dbgcmd
||1:1:017> ||1s
||1:1:017> ||
   0 User mini dump: c:\notepad.dmp
.  1 User mini dump: c:\paint.dmp
   2 User mini dump: c:\calc.dmp
```

查看完当前转储文件后，可以使用 [detach](-detach--detach-from-process-.md) 命令。

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

有关调试的其他信息，请参阅以下资源。

**书籍**

- Mario Hewardt 和 Daniel Pravat 的高级 Windows 调试

- 在 Windows 调试中：通过 Tarik Soulami 在 Windows 中调试和跟踪策略的实用指南

- Windows 内部 Pavel Yosifovich、Alex Ionescu、Mark Russinovich 和 David 

**视频**

碎片整理工具显示 WinDbg 剧集13-29 [https://channel9.msdn.com/Shows/Defrag-Tools](https://channel9.msdn.com/Shows/Defrag-Tools) 










