---
title: 控制线程和进程
description: 控制线程和进程
keywords:
- 调试器引擎 API、线程和进程
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcca7b0c69448a00626618c2135eb5ea539caef5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833685"
---
# <a name="controlling-threads-and-processes"></a>控制线程和进程


## <span id="ddk_threads_and_processes_dbx"></span><span id="DDK_THREADS_AND_PROCESSES_DBX"></span>


有关调试器引擎中的线程和进程的概述，请参阅 [线程和进程](threads-and-processes.md)。

事件发生时，事件线程和事件进程将设置为线程，并处理发生事件 (操作系统或虚拟) 。 它们分别可通过 [**GetEventThread**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-geteventthread) 和 [**GetEventProcess**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-geteventprocess)找到。

### <a name="span-idimplicit_threads_and_processesspanspan-idimplicit_threads_and_processesspanimplicit-threads-and-processes"></a><span id="implicit_threads_and_processes"></span><span id="IMPLICIT_THREADS_AND_PROCESSES"></span>隐式线程和进程

在内核模式调试中，调试器引擎将使用 *隐式进程* 来确定执行虚拟到物理地址转换时要使用的虚拟地址空间，例如，在方法 [**VirtualToPhysical**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-virtualtophysical) 和 [**ReadVirtual**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readvirtual)中。 事件发生时，隐式进程将设置为当前进程。

可以使用 [**SetImplicitProcessDataOffset**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-setimplicitprocessdataoffset)更改隐式进程。 若要确定隐式进程，请使用 [**GetImplicitProcessDataOffset**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getimplicitprocessdataoffset)。

**注意**   在实时内核调试会话期间设置 [断点](multiprocessor-syntax.md#breakpoints) 时，调试器引擎会将断点的虚拟地址传递给目标，目标将设置断点。 在这种情况下，仅在处理断点时使用目标的进程上下文;隐式进程的值是不相关的。

 

在内核模式调试中，调试器引擎将使用 *隐式线程* 来确定目标的某些 [寄存器](x86-architecture.md#registers)。 这包括处理器堆栈 (参阅 [**GetStackOffset**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getstackoffset)) 、帧偏移 (参阅 [**GetFrameOffset**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getframeoffset)) 和指令偏移 (参见 [**GetInstructionOffset**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getinstructionoffset)) 。 事件发生时，隐式线程设置为当前线程。

可以使用 [**SetImplicitThreadDataOffset**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-setimplicitthreaddataoffset)更改隐式线程。 若要确定隐式线程，请使用 [**GetImplicitThreadDataOffset**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getimplicitthreaddataoffset)。

并非所有寄存器都由隐式线程确定。 当隐式线程发生变化时，一些寄存器将保持不变。

**警告**   隐式进程和隐式线程是独立的。 如果隐式线程不属于隐式进程，则隐式线程的用户和会话状态将位于错误的虚拟地址空间中，尝试访问此信息会导致错误或提供错误的结果。 访问内核内存时不会出现此问题，因为内核内存地址在所有虚拟地址空间中都是固定的。 因此，可以独立于隐式进程访问位于核心内存中的隐式线程的信息。

 

### <a name="span-idthreadsspanspan-idthreadsspanthreads"></a><span id="threads"></span><span id="THREADS"></span>线程

*引擎线程 ID* 由调试器引擎用来标识每个操作系统线程和一个目标的每个虚拟线程。

当目标停止时，每个线程还会有一个相对于其所属进程的索引。 对于任何进程，进程中第一个线程的索引为零，最后一个线程的索引为进程中的线程数减一。 可以通过使用 [**GetNumberThreads**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getnumberthreads)找到当前进程中的线程数。 可以使用 [**GetTotalNumberThreads**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-gettotalnumberthreads)查找当前目标中所有进程中的线程总数。

当前进程中的一个或多个线程的引擎线程 ID 和系统线程 ID 可通过使用 [**GetThreadIdsByIndex**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getthreadidsbyindex)从其索引中找到。

引擎维护有关每个线程的几个信息。 此信息可能会查询当前线程，并可用于查找线程的引擎线程 ID。

<span id="system_thread_ID__user-mode_debugging_only_"></span><span id="system_thread_id__user-mode_debugging_only_"></span><span id="SYSTEM_THREAD_ID__USER-MODE_DEBUGGING_ONLY_"></span>系统线程 ID (仅) 用户模式调试  
可以通过使用 [**GetCurrentThreadSystemId**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentthreadsystemid)找到当前线程的系统线程 ID。 对于给定的系统线程 ID，可以使用 [**GetThreadIdBySystemId**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getthreadidbysystemid)找到相应的引擎线程 id。

<span id="thread_environment_block__TEB_"></span><span id="thread_environment_block__teb_"></span><span id="THREAD_ENVIRONMENT_BLOCK__TEB_"></span>线程环境块 (TEB)   
可以通过使用 [**GetCurrentThreadTeb**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentthreadteb)找到当前线程的 TEB 的地址。 对于给定的 TEB 地址，可通过使用 [**GetThreadIdByTeb**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getthreadidbyteb)找到相应的引擎线程 ID。 在内核模式调试中， (虚拟) 线程的 TEB 是上一事件发生时在相应处理器上运行的系统线程的 TEB。

<span id="data_offset"></span><span id="DATA_OFFSET"></span>数据偏移量  
在用户模式调试中， (系统) 线程的数据偏移量是该线程的 TEB 的位置。 在内核模式下，调试 (虚拟) 线程的数据偏移量是在上一次发生事件时，在相应处理器上运行的系统线程的 KTHREAD 结构。 可以使用 [**GetCurrentThreadDataOffset**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentthreaddataoffset)查找当前线程的数据偏移量。 对于给定的数据偏移量，可以使用 [**GetThreadIdByDataOffset**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getthreadidbydataoffset)找到相应的引擎线程 ID。

<span id="system_handle"></span><span id="SYSTEM_HANDLE"></span>系统句柄  
可以通过使用 [**GetCurrentThreadHandle**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentthreadhandle)找到当前线程的系统句柄。 对于给定的系统句柄，可使用 [**GetThreadIdByHandle**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getthreadidbyhandle)找到相应的引擎线程 ID。 在内核模式调试中，将为每个 (虚拟) 进程创建人工句柄。 此句柄仅可用于调试器引擎 API 查询。

### <a name="span-idprocessesspanspan-idprocessesspanprocesses"></a><span id="processes"></span><span id="PROCESSES"></span>工艺

调试器引擎使用 *引擎进程 ID* 来识别每个操作系统进程和目标的每个虚拟进程。

当目标停止时，每个进程都有一个相对于目标的索引。 目标中第一个进程的索引为零，最后一个进程的索引为目标中的进程数减一。 可以使用 [**GetNumberProcesses**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getnumberprocesses)查找当前目标中的进程数。

可以使用 [**GetProcessIdsByIndex**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getprocessidsbyindex)从其索引中找到当前目标中的一个或多个线程的引擎进程 id 和系统进程 id。

引擎维护有关每个进程的几个信息。 此信息可能会查询当前进程，并且可用于查找进程的引擎进程 ID。

<span id="system_process_ID__user-mode_debugging_only_"></span><span id="system_process_id__user-mode_debugging_only_"></span><span id="SYSTEM_PROCESS_ID__USER-MODE_DEBUGGING_ONLY_"></span>系统进程 ID (仅限用户模式调试)   
可以使用 [**GetCurrentProcessSystemId**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentprocesssystemid)查找当前进程的系统进程 ID。 对于给定的系统进程 ID，可以使用 [**GetProcessIdBySystemId**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getprocessidbysystemid)找到相应的引擎进程 id。

<span id="process_environment_block__PEB_"></span><span id="process_environment_block__peb_"></span><span id="PROCESS_ENVIRONMENT_BLOCK__PEB_"></span>进程环境块 (PEB)   
可以通过使用 [**GetCurrentProcessPeb**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentprocesspeb)查找当前进程的 PEB 的地址。 对于给定的 PEB 地址，可通过使用 [**GetProcessIdByPeb**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getprocessidbypeb)找到相应的引擎进程 ID。 在内核模式调试中， (虚拟) 进程的 PEB 是在上一次发生事件时运行的系统进程的 PEB。

<span id="data_offset"></span><span id="DATA_OFFSET"></span>数据偏移量  
在用户模式调试中， (系统) 进程的数据偏移量是该进程的 PEB 的位置。 在内核模式调试中， (虚拟) 进程的数据偏移量是在上一次发生事件时运行的系统进程的 KPROCESS 结构。 可以使用 [**GetCurrentProcessDataOffset**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentprocessdataoffset)查找当前进程的数据偏移量。 对于给定的数据偏移量，可以使用 [**GetProcessIdByDataOffset**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getprocessidbydataoffset)找到相应的引擎进程 ID。

<span id="system_handle"></span><span id="SYSTEM_HANDLE"></span>系统句柄  
可以使用 [**GetCurrentProcessHandle**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentprocesshandle)查找当前进程的系统句柄。 对于给定的系统句柄，可使用 [**GetProcessIdByHandle**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getprocessidbyhandle)找到相应的引擎进程 ID。 在内核模式调试中，为 (虚拟) 进程创建人工句柄。 此句柄仅可用于调试器引擎查询。

### <a name="span-ideventsspanspan-ideventsspanevents"></a><span id="events"></span><span id="EVENTS"></span>事件

在实时用户模式调试中，只要在目标中创建或退出线程，就会生成 "创建线程" 和 "退出线程" 调试事件。 这些事件将导致调用 [**IDebugEventCallbacks：： CreateThread**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugeventcallbacks-createthread) 和 [**IDebugEventCallbacks：： ExitThread**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugeventcallbacks-exitthread) 回调方法。

在实时用户模式调试中，只要在目标中创建或退出进程，就会生成创建进程和退出进程调试事件。 这些事件将导致调用 [**IDebugEventCallbacks：： CreateProcess**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugeventcallbacks-createprocess) 和 [**IDebugEventCallbacks：： ExitProcess**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugeventcallbacks-exitprocess) 回调方法。

有关事件的详细信息，请参阅 [监视事件](monitoring-events.md)。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关线程和进程的详细信息，包括 TEB、KTHREAD、PEB 和 KPROCESS 结构，请参阅 David 所罗门群岛的 *Microsoft Windows 内部机制* 和标记 Russinovich。

 

