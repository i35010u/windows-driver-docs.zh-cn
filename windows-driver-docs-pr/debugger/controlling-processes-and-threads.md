---
title: 控制进程和线程
description: 控制进程和线程
keywords:
- 进程
- 进程，选择
- 线程 (thread)
- 线程，选择
- 线程，冻结
- 'thread、解冻 (解冻) '
- 线程，暂停
- 挂起线程计数
- 冻结线程
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed65704123825818885bffe3428f007b89d08d80
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787825"
---
# <a name="controlling-processes-and-threads"></a>控制进程和线程


## <span id="ddk_controlling_processes_and_threads_dbg"></span><span id="DDK_CONTROLLING_PROCESSES_AND_THREADS_DBG"></span>


执行用户模式调试时，可以激活、显示、冻结、取消冻结、挂起和取消挂起进程和线程。

*当前* 进程或 *活动* 进程是当前正在调试的进程。 同样， *当前* 线程或 *活动* 线程是调试器当前控制的线程。 许多调试器命令的操作由当前进程和线程的标识确定。 当前进程还确定调试器使用的虚拟地址映射。

调试开始时，当前进程是调试器附加到的进程，或者是导致中断到调试器中的异常的进程。 同样，当前线程是在调试器附加到进程或导致异常的情况下处于活动状态的线程。 但是，可以使用调试器更改当前进程和线程，并冻结或解冻单个线程。

在内核模式调试中，进程和线程不受此部分中所述的方法控制。 有关如何在内核模式下操作进程和线程的详细信息，请参阅 [更改上下文](changing-contexts.md)。

### <a name="span-iddisplaying_processes_and_threadsspanspan-iddisplaying_processes_and_threadsspandisplaying-processes-and-threads"></a><span id="displaying_processes_and_threads"></span><span id="DISPLAYING_PROCESSES_AND_THREADS"></span>显示进程和线程

若要显示进程和线程信息，可以使用以下方法：

-   [**| (进程状态)**](---process-status-.md)命令

-   [**~ (线程状态)**](---thread-status-.md)命令

-   仅 (WinDbg) " [进程和线程" 窗口](processes-and-threads-window.md)

### <a name="span-idsetting_the_current_process_and_threadspanspan-idsetting_the_current_process_and_threadspansetting-the-current-process-and-thread"></a><span id="setting_the_current_process_and_thread"></span><span id="SETTING_THE_CURRENT_PROCESS_AND_THREAD"></span>设置当前进程和线程

若要更改当前进程或线程，可以使用以下方法：

-   [**| S (设置当前进程)**](-s--set-current-process-.md)命令

-   [**~ S (设置当前线程)**](-s--set-current-thread-.md)命令

-   仅 (WinDbg) " [进程和线程" 窗口](processes-and-threads-window.md)

### <a name="span-idfreezing_and_suspending_threadsspanspan-idfreezing_and_suspending_threadsspanfreezing-and-suspending-threads"></a><span id="freezing_and_suspending_threads"></span><span id="FREEZING_AND_SUSPENDING_THREADS"></span>冻结和挂起线程

调试器可以通过 *挂起* 线程或 *冻结* 线程来更改线程的执行。 这两个操作的效果略有不同。

每个线程都具有与之关联的 *挂起计数* 。 如果此计数为1或更大，则系统不会运行该线程。 如果计数为零或更低，则系统将在适当的时候运行线程。

通常，每个线程的挂起计数都为零。 调试器附加到进程时，会将该进程中的所有线程的挂起计数增加一。 如果调试器从进程中分离，则它会将所有挂起计数减1。 调试器执行该过程时，它会暂时将所有挂起计数递减1。

可以通过使用以下方法来控制调试器中任何线程的挂起计数：

-   [**~ N (挂起线程)**](-n--suspend-thread-.md)命令将指定线程的挂起计数增加一。

-   [**~ M (Resume 线程)**](-m--resume-thread-.md)命令将指定线程的挂起计数减一。

这些命令最常见的用途是将特定线程的挂起计数从1个提升到2个。 调试器执行或分离进程时，该线程会将挂起计数为1，并保持挂起状态，即使进程中的其他线程正在执行。

即使执行 [noninvasive 调试](noninvasive-debugging--user-mode-.md)，也可以挂起线程。

调试器还可以 *冻结* 线程。 此操作类似于以某些方式挂起线程。 但是，"冻结" 只是一个调试器设置。 Windows 操作系统中的任何内容都无法识别此线程的任何不同之处。

默认情况下，所有线程都未冻结。 当调试器导致进程执行时，冻结的线程不会执行。 但是，如果调试器从进程中分离出来，则所有线程都将取消冻结。

若要冻结和解冻单个线程，可以使用以下方法：

-   [**~ F (冻结线程)**](-f--freeze-thread-.md)命令冻结指定线程。

-   [**~ U (取消冻结线程)**](-u--unfreeze-thread-.md)命令 unfreezes 指定线程。

在任何情况下，属于目标进程的线程在调试器已分解到目标时永远不会执行。 仅当调试器执行进程或分离时，线程的挂起计数才会影响线程的行为。 仅当调试器执行进程时，冻结状态才会影响线程的行为。

### <a name="span-idthreads_and_processes_in_other_commandsspanspan-idthreads_and_processes_in_other_commandsspanthreads-and-processes-in-other-commands"></a><span id="threads_and_processes_in_other_commands"></span><span id="THREADS_AND_PROCESSES_IN_OTHER_COMMANDS"></span>其他命令中的线程和进程

可以在许多其他命令之前添加线程说明符或进程说明符。 有关详细信息，请参阅各个命令主题。

你可以在多个命令和扩展命令之前添加 [**~ e (线程特定的命令)**](-e--thread-specific-command-.md) 限定符。 此限定符会使命令在指定的线程上执行。 如果要将一个命令应用于多个线程，此限定符特别有用。 例如，以下命令对每个正在调试的线程重复 [**！ gle**](-gle.md) extension 命令。

```dbgcmd
~*e !gle 
```

### <a name="span-idmultiple_systemsspanspan-idmultiple_systemsspanmultiple-systems"></a><span id="multiple_systems"></span><span id="MULTIPLE_SYSTEMS"></span>多个系统

调试器可以同时附加到多个目标。 如果这些进程包含转储文件或在多台计算机上包含实时目标，则调试器将为每个操作引用系统、进程和线程。 有关此类调试的详细信息，请参阅 [调试多个目标](debugging-multiple-targets.md)。

 

 





