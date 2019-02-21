---
title: 控制进程和线程
description: 控制进程和线程
ms.assetid: f5a50b54-443e-425e-98cb-cff8d31ac897
keywords:
- 进程
- 处理，请选择
- 线程
- 选择的线程
- 冻结线程
- 线程，解除冻结 （解冻）
- 挂起的线程
- 挂起线程的计数
- 冻结线程
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21fafe94ccd6d6b262b2505cc00b83ff640a3209
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526359"
---
# <a name="controlling-processes-and-threads"></a>控制进程和线程


## <span id="ddk_controlling_processes_and_threads_dbg"></span><span id="DDK_CONTROLLING_PROCESSES_AND_THREADS_DBG"></span>


执行用户模式下时调试，你激活、 显示、 冻结、 解冻、 挂起，和取消挂起进程和线程。

*当前*或*active*过程是当前正在调试的进程。 同样，*当前*或*active*线程是调试器当前控制的线程。 许多调试器命令的操作决定由当前进程和线程标识。 当前进程还确定调试器使用的虚拟地址映射。

当调试开始时，当前进程是一个调试器附加到或导致调试器中分解的异常。 同样，当前线程是一个调试器附加到进程或引发异常时处于活动状态。 但是，可以使用调试器更改当前进程和线程还可以冻结或解冻各个线程。

在内核模式调试、 进程和线程不受此部分所述的方法。 有关如何在内核模式下操作进程和线程的详细信息，请参阅[更改上下文](changing-contexts.md)。

### <a name="span-iddisplayingprocessesandthreadsspanspan-iddisplayingprocessesandthreadsspandisplaying-processes-and-threads"></a><span id="displaying_processes_and_threads"></span><span id="DISPLAYING_PROCESSES_AND_THREADS"></span>显示进程和线程

若要显示进程和线程信息，可以使用以下方法：

-   [ **|（进程状态）** ](---process-status-.md)命令

-   [ **~ （线程状态）** ](---thread-status-.md)命令

-   (仅 WinDbg)[进程和线程窗口](processes-and-threads-window.md)

### <a name="span-idsettingthecurrentprocessandthreadspanspan-idsettingthecurrentprocessandthreadspansetting-the-current-process-and-thread"></a><span id="setting_the_current_process_and_thread"></span><span id="SETTING_THE_CURRENT_PROCESS_AND_THREAD"></span>设置当前进程和线程

若要更改的当前进程或线程，您可以使用以下方法：

-   [ **| S （设置当前进程）** ](-s--set-current-process-.md)命令

-   [ **~ （设置当前线程） s** ](-s--set-current-thread-.md)命令

-   (仅 WinDbg)[进程和线程窗口](processes-and-threads-window.md)

### <a name="span-idfreezingandsuspendingthreadsspanspan-idfreezingandsuspendingthreadsspanfreezing-and-suspending-threads"></a><span id="freezing_and_suspending_threads"></span><span id="FREEZING_AND_SUSPENDING_THREADS"></span>冻结和挂起线程

调试器可以更改的情况下，线程执行*挂起*线程或由*冻结*线程。 这两个操作具有某种程度上不同的作用。

每个线程都具有*挂起计数*与它相关联。 如果此计数是一个更大，系统不会运行该线程。 如果计数为零或更低时，系统就会运行的线程在适当的时候。

通常，每个线程的挂起计数为零。 当调试器附加到进程时，它由一个递增该进程中的所有线程的挂起计数。 如果调试器与进程分离它所有的递减一个挂起计数。 当调试器执行该过程时，它暂时递减所有挂起计数 1。

可以使用以下方法控制在调试器中的任何线程的挂起计数：

-   [ **~ N （挂起线程）** ](-n--suspend-thread-.md)命令递增指定线程的挂起计数 1。

-   [ **~ M （恢复线程）** ](-m--resume-thread-.md)命令都会减少指定的线程的挂起计数 1。

最常见的用途有关这些命令是引发特定线程的挂起计数一到两个。 当调试器执行，或与进程分离时，该线程然后已挂起计数为 1，并保持挂起状态，即使在过程中的其他线程正在执行。

甚至当正在执行时，您可以挂起线程[非侵入调试](noninvasive-debugging--user-mode-.md)。

调试器还可以*冻结*线程。 此操作是类似于在某种程度上挂起线程。 但是，"冻结"是调试器设置。 在 Windows 操作系统中为 nothing 识别出的任何内容是有关此线程不同。

默认情况下，所有线程都都未冻结。 当调试器导致一个进程来执行时，才会执行已冻结的线程。 但是，如果调试器与进程分离，取消对所有线程。

冻结和解冻各个线程，可以使用以下方法：

-   [ **~ F （冻结线程）** ](-f--freeze-thread-.md)命令冻结指定的线程。

-   [ **~ U （取消冻结线程）** ](-u--unfreeze-thread-.md)命令取消冻结指定的线程。

在任何情况下，属于目标进程的线程永远不会执行时调试器已分解为目标。 仅在调试器执行进程或分离时，线程的挂起计数会影响线程的行为。 仅当在调试器执行该过程时，冻结的状态会影响线程的行为。

### <a name="span-idthreadsandprocessesinothercommandsspanspan-idthreadsandprocessesinothercommandsspanthreads-and-processes-in-other-commands"></a><span id="threads_and_processes_in_other_commands"></span><span id="THREADS_AND_PROCESSES_IN_OTHER_COMMANDS"></span>线程和进程中的其他命令

您可以添加线程说明符或许多其他命令之前的过程说明符。 有关详细信息，请参阅单个命令主题。

您可以添加[ **~ e （特定于线程的命令）** ](-e--thread-specific-command-.md)之前许多命令和扩展命令限定符。 此限定符会导致与指定的线程执行的命令。 此限定符是特别有用，如果你想要将命令应用到多个线程。 例如，以下命令重复[ **！ gle** ](-gle.md)正在调试的每个线程的扩展命令。

```dbgcmd
~*e !gle 
```

### <a name="span-idmultiplesystemsspanspan-idmultiplesystemsspanmultiple-systems"></a><span id="multiple_systems"></span><span id="MULTIPLE_SYSTEMS"></span>多个系统

在同一时间可以将调试器附加到多个目标。 当这些进程包括转储文件或包含多台计算机上的实时目标时，调试器将引用系统、 进程和线程的每个操作。 有关调试此类的详细信息，请参阅[调试多个目标](debugging-multiple-targets.md)。

 

 





