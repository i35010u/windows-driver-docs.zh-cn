---
title: 控制线程和进程
description: 控制线程和进程
ms.assetid: 6182ca34-ee5e-47e9-82fe-29266397e3a8
keywords:
- 调试器引擎 API、 线程和进程
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea72fa364f2336d7d6fad2403af3643608ab5c3c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366998"
---
# <a name="controlling-threads-and-processes"></a>控制线程和进程


## <span id="ddk_threads_and_processes_dbx"></span><span id="DDK_THREADS_AND_PROCESSES_DBX"></span>


线程和进程在调试器引擎的概述，请参阅[线程和进程](threads-and-processes.md)。

事件发生时，事件线程和事件进程设置为线程和进程 (操作系统或虚拟) 中发生该事件。 可以使用查找他们[ **GetEventThread** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-geteventthread)并[ **GetEventProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-geteventprocess)分别。

### <a name="span-idimplicitthreadsandprocessesspanspan-idimplicitthreadsandprocessesspanimplicit-threads-and-processes"></a><span id="implicit_threads_and_processes"></span><span id="IMPLICIT_THREADS_AND_PROCESSES"></span>隐式线程和进程

在内核模式调试的调试程序引擎将使用*隐式过程*用于确定要执行虚拟到物理地址转换-例如，在方法中时使用的虚拟地址空间[ **VirtualToPhysical** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-virtualtophysical)并[ **ReadVirtual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugdataspaces4-readvirtual)。 事件发生时，隐式过程设置为当前进程。

可能会使用更改隐式过程[ **SetImplicitProcessDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-setimplicitprocessdataoffset)。 若要确定隐式过程用[ **GetImplicitProcessDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getimplicitprocessdataoffset)。

**请注意**  设置时[断点](multiprocessor-syntax.md#breakpoints)期间实时内核调试会话，调试器引擎将通过断点的虚拟地址到目标，并在目标将设置断点。 当处理断点; 在这种情况下，使用仅目标的进程上下文隐式过程的值是不相关。

 

在内核模式调试中，将使用调试器引擎*隐式线程*来确定目标的一部分[注册](x86-architecture.md#registers)。 这包括处理器堆栈 (请参阅[ **GetStackOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getstackoffset))，帧偏移量 (请参阅[ **GetFrameOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getframeoffset))，和说明偏移量 (请参阅[ **GetInstructionOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getinstructionoffset))。 事件发生时，隐式线程设置为当前线程。

隐式线程可能会更改通过使用[ **SetImplicitThreadDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-setimplicitthreaddataoffset)。 若要确定隐式线程，请使用[ **GetImplicitThreadDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getimplicitthreaddataoffset)。

并非所有寄存器由隐式线程都确定。 某些寄存器隐式线程发生更改时将保持不变。

**警告**  隐式过程和隐式线程是独立的。 如果隐式线程不属于隐式的过程，然后将处于错误的虚拟地址空间的用户和会话状态的隐式线程，并尝试访问此信息将会导致错误或提供不正确的结果。 访问内核内存，因为内核内存地址跨所有虚拟地址空间是不变时不会出现此问题。 因此可以访问隐式线程位于内核内存中的信息独立于隐式过程。

 

### <a name="span-idthreadsspanspan-idthreadsspanthreads"></a><span id="threads"></span><span id="THREADS"></span>线程

*引擎线程 ID*调试器引擎用于标识每个操作系统线程和目标的每个虚拟线程。

当停止目标时，每个线程还具有相对于其所属的进程的索引。 为任何进程的过程中的第一个线程索引为零，并最后一个线程的索引是减一进程中的线程数。 可以使用找到的当前进程中的线程数[ **GetNumberThreads**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getnumberthreads)。 可以使用找到的当前目标中的所有进程中的线程总数[ **GetTotalNumberThreads**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-gettotalnumberthreads)。

可以通过使用从其索引找到引擎线程 ID 和系统线程 ID 的当前进程中的一个或多个线程[ **GetThreadIdsByIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getthreadidsbyindex)。

引擎会保留以下几条有关每个线程的信息。 此信息可能不会查询当前线程，并可用于查找一个线程的引擎线程 ID。

<span id="system_thread_ID__user-mode_debugging_only_"></span><span id="system_thread_id__user-mode_debugging_only_"></span><span id="SYSTEM_THREAD_ID__USER-MODE_DEBUGGING_ONLY_"></span>系统线程 ID （仅限调试模式下的用户）  
可以使用找到的当前线程的系统线程 ID [ **GetCurrentThreadSystemId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentthreadsystemid)。 对于给定的系统线程 ID，可能通过找到相应的引擎线程 ID [ **GetThreadIdBySystemId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getthreadidbysystemid)。

<span id="thread_environment_block__TEB_"></span><span id="thread_environment_block__teb_"></span><span id="THREAD_ENVIRONMENT_BLOCK__TEB_"></span>线程环境块 (TEB)  
可以使用找到的地址对于当前线程 TEB [ **GetCurrentThreadTeb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentthreadteb)。 对于给定的 TEB 地址，可能通过使用找到相应的引擎线程 ID [ **GetThreadIdByTeb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getthreadidbyteb)。 在内核模式调试中，（虚拟） 线程的 TEB 是最后一个事件发生时正在运行相应的处理器上的系统线程 TEB。

<span id="data_offset"></span><span id="DATA_OFFSET"></span>数据偏移量  
在用户模式下调试中，（系统） 线程的数据偏移量是该线程 TEB 的位置。 在内核模式下调试数据 （虚拟） 线程的偏移量是最后一个事件发生时正在运行相应的处理器的系统线程 KTHREAD 结构。 可以使用找到的当前线程的数据偏移量[ **GetCurrentThreadDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentthreaddataoffset)。 给定的数据偏移量，可能通过找到相应的引擎线程 ID [ **GetThreadIdByDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getthreadidbydataoffset)。

<span id="system_handle"></span><span id="SYSTEM_HANDLE"></span>系统句柄  
可以使用找到的当前线程的系统句柄[ **GetCurrentThreadHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentthreadhandle)。 为给定的系统句柄对应的引擎线程 ID 可能会找到通过使用[ **GetThreadIdByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getthreadidbyhandle)。 在内核模式调试，为每个 （虚拟） 进程创建人工句柄。 此句柄仅可用于调试器引擎 API 查询。

### <a name="span-idprocessesspanspan-idprocessesspanprocesses"></a><span id="processes"></span><span id="PROCESSES"></span>进程

*引擎进程 ID*调试器引擎用于标识每个操作系统进程和目标的每个虚拟进程。

当停止目标时，每个进程具有与目标索引。 目标中的第一个过程的索引为 0，，最后一个进程的索引为减一目标中的进程数。 可以使用找到的进程中的当前目标数[ **GetNumberProcesses**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getnumberprocesses)。

通过使用情况下，当前的目标中的一个或多个线程的引擎进程 ID 和系统进程 ID 可以找到从它们的索引[ **GetProcessIdsByIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getprocessidsbyindex)。

引擎会保留以下几条有关每个进程的信息。 此信息可能不会查询当前进程，并可用于为进程查找引擎进程 ID。

<span id="system_process_ID__user-mode_debugging_only_"></span><span id="system_process_id__user-mode_debugging_only_"></span><span id="SYSTEM_PROCESS_ID__USER-MODE_DEBUGGING_ONLY_"></span>系统进程 ID （仅限调试模式下的用户）  
可以使用找到的当前进程的系统进程 ID [ **GetCurrentProcessSystemId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentprocesssystemid)。 对于给定的系统进程 ID，可能通过找到相应的引擎进程 ID [ **GetProcessIdBySystemId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getprocessidbysystemid)。

<span id="process_environment_block__PEB_"></span><span id="process_environment_block__peb_"></span><span id="PROCESS_ENVIRONMENT_BLOCK__PEB_"></span>进程环境块 (PEB)  
可以使用找到的地址为当前进程 PEB [ **GetCurrentProcessPeb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentprocesspeb)。 对于给定的 PEB 地址，可能通过找到相应的引擎进程 ID [ **GetProcessIdByPeb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getprocessidbypeb)。 在内核模式调试中，（虚拟） 进程的 PEB 是最后一个事件发生时正在运行的系统进程 PEB。

<span id="data_offset"></span><span id="DATA_OFFSET"></span>数据偏移量  
在用户模式下调试中，（系统） 进程的数据偏移量是该过程的 PEB 的位置。 在内核模式调试下 （虚拟） 进程的数据偏移量是最后一个事件发生时正在运行的系统进程的 KPROCESS 结构。 可以使用找到的当前进程的数据偏移量[ **GetCurrentProcessDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentprocessdataoffset)。 给定的数据偏移量，可能通过找到相应的引擎进程 ID [ **GetProcessIdByDataOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getprocessidbydataoffset)。

<span id="system_handle"></span><span id="SYSTEM_HANDLE"></span>系统句柄  
可以使用找到的当前进程的系统句柄[ **GetCurrentProcessHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentprocesshandle)。 为给定的系统句柄对应的引擎进程 ID 可能找到通过使用[ **GetProcessIdByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugsystemobjects4-getprocessidbyhandle)。 在内核模式调试，人工句柄创建 （虚拟） 的过程。 此句柄仅可用于调试器引擎查询。

### <a name="span-ideventsspanspan-ideventsspanevents"></a><span id="events"></span><span id="EVENTS"></span>事件

实时用户模式调试中，创建一个线程时或在目标中，创建线程并退出线程退出中生成调试事件。 这些事件会导致调用[ **IDebugEventCallbacks::CreateThread** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugeventcallbacks-createthread)并[ **IDebugEventCallbacks::ExitThread** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugeventcallbacks-exitthread)回叫方法。

在实时用户模式下调试时将创建一个进程或退出目标中的，生成的创建过程和退出过程的调试事件。 这些事件会导致调用[ **IDebugEventCallbacks::CreateProcess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugeventcallbacks-createprocess)并[ **IDebugEventCallbacks::ExitProcess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugeventcallbacks-exitprocess)回叫方法。

有关事件的详细信息，请参阅[监视事件](monitoring-events.md)。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关线程和进程，包括 TEB、 KTHREAD、 PEB 和 KPROCESS 结构的详细信息请参阅*Microsoft Windows Internals*由 David Solomon 和 Mark Russinovich。

 

 





