---
title: 编写 Bug 检查原因回调例程
description: 编写 Bug 检查回调例程
keywords:
- bug 检查回调例程 WDK 内核
- 回调例程 WDK bug 检查
- 注册回调例程
- KeRegisterBugCheckCallback
- BugCheckCallback
ms.date: 05/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5de8c356cd0e2e9d5a06570a185dc677c6208091
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782639"
---
# <a name="writing-a-bug-check-reason-callback-routine"></a>编写 Bug 检查原因回调例程

驱动程序可以选择提供一个 [*KBUGCHECK_REASON_CALLBACK_ROUTINE*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_reason_callback_routine) 回调函数，该函数在写入故障转储文件后，系统会调用此函数。

> [!NOTE]
> 本文介绍 bug 检查 *原因* 回调例程，而不是 [*KBUGCHECK_CALLBACK_ROUTINE*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_callback_routine) 回调函数。

在此回调中，驱动程序可以：

* 向崩溃转储文件添加驱动程序特定的数据
* 将设备重置为已知状态

使用以下例程注册并删除回调：

* [**KeRegisterBugCheckReasonCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback)
* [**KeDeregisterBugCheckReasonCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback)

此回调类型会重载，并根据注册时所提供的 [**KBUGCHECK_CALLBACK_REASON**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_kbugcheck_callback_reason) 常数值发生更改。  本文介绍了不同的使用方案。

有关 bug 检查数据的一般信息，请参阅 [读取 Bug 检查回调数据](../debugger/reading-bug-check-callback-data.md)。

## <a name="bug-check-callback-routine-restrictions"></a>Bug 检查回调例程限制

Bug 检查回调例程在 IRQL = 高级别执行 \_ ，这对它的功能施加了严格的限制。

Bug 检查回调例程不能：

* 分配内存
* 访问可分页内存
* 使用任何同步机制
* 调用必须在 IRQL = 调度 \_ 级别或下面执行的任何例程

Bug 检查回调例程保证在不中断的情况下运行，因此无需同步。  (如果 bug 检查例程确实使用任何同步机制，则系统会死锁。 ) 

驱动程序的 bug 检查回调例程可以安全地使用 **读取 \_ 端口 \_ <em>xxx</em>**，**读取 \_ register \_ <em>xxx</em>**，**写入 \_ 端口 \_ <em>xxx</em>**，并 **写入 \_ register \_ <em>xxx</em>** 例程以与驱动程序的设备进行通信。 有关这些例程的信息 (，请参阅 [硬件抽象层例程](/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))。 ) 

## <a name="implementing-a-kbcallbackaddpages-callback-routine"></a>实现 KbCallbackAddPages 回调例程

内核模式驱动程序可以实现 <i>KbCallbackAddPages</i>类型的 [*KBUGCHECK_REASON_CALLBACK_ROUTINE*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_reason_callback_routine)回调函数，以便在发生 bug 检查时将一个或多个数据页添加到故障转储文件中。 若要在操作系统中注册此例程，驱动程序将调用 <b><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback">KeRegisterBugCheckReasonCallback</a></b> 例程。 卸载驱动程序之前，必须调用 <b><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback">KeDeregisterBugCheckReasonCallback</a></b> 例程以删除注册。

从 Windows 8 开始，在<a href="/windows-hardware/drivers/debugger/kernel-memory-dump">内核内存转储</a>或<a href="/windows-hardware/drivers/debugger/complete-memory-dump">完整内存转储</a>期间调用已注册的<i>KbCallbackAddPages</i>例程。 在较早版本的 Windows 中，在内核内存转储期间调用已注册的 <i>KbCallbackAddPages</i> 例程，而不是在完整内存转储过程中调用。 默认情况下，内核内存转储只包含 Windows 内核在发生 bug 检查时使用的物理页面，而完整的内存转储包含 Windows 使用的所有物理内存。 默认情况下，完全内存转储不包括平台固件使用的物理内存。

<i>KbCallbackAddPages</i>例程可以提供要添加到转储文件的特定于驱动程序的数据。 例如，对于内核内存转储，这额外的数据可能包含未映射到虚拟内存中的系统地址范围的物理页面，但包含有助于调试驱动程序的信息。 <i>KbCallbackAddPages</i>例程可能会向转储文件添加未映射的任何驱动程序拥有的物理页面，或映射到虚拟内存中的用户模式地址的任何驱动程序。

发生 bug 检查时，操作系统将调用所有已注册的 <i>KbCallbackAddPages</i> 例程，以轮询驱动程序以将数据添加到故障转储文件。 每次调用都会向崩溃转储文件中添加一个或多个连续数据页。 <i>KbCallbackAddPages</i>例程可以为起始页提供虚拟地址或物理地址。 如果在调用过程中提供了多个页，则这些页在虚拟或物理内存中是连续的，具体取决于起始地址是虚拟的还是物理的。 若要提供非连续页面， <i>KbCallbackAddPages</i> 例程可以在 <b><a href="/windows-hardware/drivers/ddi/wdm/ns-wdm-_kbugcheck_add_pages">KBUGCHECK_ADD_PAGES</a></b> 结构中设置标志，以指示该标志包含其他数据并且必须再次调用。

与将数据追加到辅助故障转储区域的 *KbCallbackSecondaryDumpData* 例程不同， <i>KbCallbackAddPages</i> 例程将数据页添加到主故障转储区域。 在调试期间，主故障转储数据比辅助故障转储数据更易于访问。

操作系统将填充<i>ReasonSpecificData</i>指向的<b>KBUGCHECK_ADD_PAGES</b>结构的<b>BugCheckCode</b>成员。 <i>KbCallbackAddPages</i>例程必须设置此结构的<b>Flags</b>、 <b>Address</b>和<b>Count</b>成员的值。

在首次调用 <i>KbCallbackAddPages</i>之前，操作系统会将 <b>上下文</b> 初始化为 <b>NULL</b>。 如果多次调用 <i>KbCallbackAddPages</i> 例程，操作系统将保留回调例程写入上一个调用中的 <b>上下文</b> 成员的值。

<i>KbCallbackAddPages</i>例程非常受限于它可以执行的操作。 有关详细信息，请参阅 [Bug 检查回调例程限制](#bug-check-callback-routine-restrictions)。

## <a name="implementing-a-kbcallbackdumpio-callback-routine"></a>实现 KbCallbackDumpIo 回调例程

内核模式驱动程序可以实现 <i>KbCallbackDumpIo</i>类型的 [*KBUGCHECK_REASON_CALLBACK_ROUTINE*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_reason_callback_routine)回调函数，以便在每次将数据写入故障转储文件时执行工作。 系统将在 <i>ReasonSpecificData</i> 参数中传递一个指向 [**KBUGCHECK_DUMP_IO**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_kbugcheck_dump_io) 结构的指针。 <b>缓冲区</b>成员指向当前数据， <b>BufferLength</b>成员指定其长度。 <b>类型</b>成员指示当前写入的数据类型，例如转储文件头信息、内存状态或驱动程序提供的数据。 有关可能的信息类型的说明，请参阅 <b><a href="/windows-hardware/drivers/ddi/wdm/ne-wdm-_kbugcheck_dump_io_type">KBUGCHECK_DUMP_IO_TYPE</a></b> 枚举。

系统可以按顺序或按顺序写入故障转储文件。 如果系统按顺序写入故障转储文件，则<i>ReasonSpecificData</i>的<b>Offset</b>成员为-1;否则，<b>偏移量</b>设置为故障转储文件中的当前偏移量（以字节为单位）。

当系统按顺序写入文件时，它会调用每个<i>KbCallbackDumpIo</i>例程一次或多次写入标头信息 (<b>类型</b>  =  <b>KbDumpIoHeader</b>) ，写入故障转储文件的主体 (<b>类型</b>KbDumpIoBody) 时，一次或多次，写入  =  <b>KbDumpIoBody</b>辅助转储数据 (<b>类型</b>  =  <b>KbDumpIoSecondaryDumpData</b>) 。 系统完成写入故障转储文件后，它将调用<b>缓冲区</b>  =  <b>为 NULL</b>、 <b>BufferLength</b> = 0 且<b>类型</b>为  =  <b>KbDumpIoComplete</b>的回调。

<i>KbCallbackDumpIo</i>例程的主要目的是允许将系统崩溃转储数据写入磁盘以外的其他设备。 例如，监视系统状态的设备可以使用回调报告系统已发出 bug 检查，并为分析提供故障转储。

使用 <b><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback">KeRegisterBugCheckReasonCallback</a></b> 注册 <i>KbCallbackDumpIo</i> 例程。 然后，驱动程序可以使用 <b><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback">KeDeregisterBugCheckReasonCallback</a></b> 例程删除回调。 如果可以卸载该驱动程序，则必须在其 <i><a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload">DRIVER_UNLOAD</a></i> 回调函数中删除所有已注册的回调。

在可执行的操作中， <i>KbCallbackDumpIo</i> 例程受到严格限制。 有关详细信息，请参阅 [Bug 检查回调例程限制](#bug-check-callback-routine-restrictions)。

## <a name="implementing-a-kbcallbacksecondarydumpdata-callback-routine"></a>实现 KbCallbackSecondaryDumpData 回调例程

内核模式驱动程序可以实现 <i>KbCallbackSecondaryDumpData</i>类型的 [*KBUGCHECK_REASON_CALLBACK_ROUTINE*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_reason_callback_routine)回调函数，以提供要追加到故障转储文件的数据。

系统将设置<b>InBuffer</b>、 <b>InBufferLength</b>、 <b>OutBuffer</b>和<b>MaximumAllowed</b>成员作为<i>ReasonSpecificData</i>指向的<b><a href="/windows-hardware/drivers/ddi/wdm/ns-wdm-_kbugcheck_secondary_dump_data">KBUGCHECK_SECONDARY_DUMP_DATA</a></b>结构。 <b>MaximumAllowed</b>成员指定例程可以提供的最大转储数据量。

<b>OutBuffer</b>成员的值确定系统是请求驱动程序的转储数据还是数据本身，如下所示：

* 如果 KBUGCHECK_SECONDARY_DUMP_DATA 的 <b>OutBuffer</b> 成员为 <b>NULL</b>，则系统只请求大小信息。 <i>KbCallbackSecondaryDumpData</i>例程填充<b>OutBuffer</b>和<b>OutBufferLength</b>成员。 
* 如果 KBUGCHECK_SECONDARY_DUMP_DATA 的 <b>OutBuffer</b> 成员等于 <b>InBuffer</b> 成员，则系统将请求驱动程序的辅助转储数据。 <i>KbCallbackSecondaryDumpData</i>例程填充<b>OutBuffer</b>和<b>OutBufferLength</b>成员，并将数据写入<b>OutBuffer</b>指定的缓冲区。

KBUGCHECK_SECONDARY_DUMP_DATA 的 <b>InBuffer</b> 成员指向用于例程的小缓冲区。 <b>InBufferLength</b>成员指定缓冲区的大小。 如果要写入的数据量小于 <b>InBufferLength</b>，则回调例程可以使用此缓冲区向系统提供故障转储数据。 然后，回调例程将 <b>OutBuffer</b> 设置为 <b>InBuffer</b> ，并将 <b>OutBufferLength</b> 设置为写入缓冲区的实际数据量。

必须写入大于 <b>InBufferLength</b> 的数据量的驱动程序可以使用自己的缓冲区来提供数据。 在执行回调例程之前，必须已分配此缓冲区，并且必须驻留在驻留内存 (如非分页池) 。 然后，回调例程将 <b>OutBuffer</b> 设置为指向驱动程序缓冲区，并将 <b>OutBufferLength</b> 到缓冲区中要写入故障转储文件的数据量。

要写入故障转储文件的每个数据块都用<b><a href="/windows-hardware/drivers/ddi/wdm/ns-wdm-_kbugcheck_secondary_dump_data">KBUGCHECK_SECONDARY_DUMP_DATA</a></b>结构的<b>Guid</b>成员的值进行标记。 所使用的 GUID 对驱动程序必须是唯一的。 若要显示与此 GUID 相对应的辅助转储数据，可以使用 <b>enumtag</b> 命令或调试器扩展中的 <b>IDebugDataSpaces3：： ReadTagged</b> 方法。 有关调试器和调试器扩展的信息，请参阅 <a href="/windows-hardware/drivers/debugger/index">Windows 调试</a>。

驱动程序可以将具有相同 GUID 的多个块写入故障转储文件，但这种做法非常糟糕，因为调试器只有第一个块可供访问。 注册多个 <i>KbCallbackSecondaryDumpData</i> 例程的驱动程序应为每个回调分配一个唯一的 GUID。

使用 <b><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckreasoncallback">KeRegisterBugCheckReasonCallback</a></b> 注册 <i>KbCallbackSecondaryDumpData</i> 例程。 然后，驱动程序可以使用 <b><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-kederegisterbugcheckreasoncallback">KeDeregisterBugCheckReasonCallback</a></b> 例程删除回调例程。 如果可以卸载该驱动程序，则必须在其 <i><a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload">DRIVER_UNLOAD</a></i> 回调函数中删除所有已注册的回调例程。

<i>KbCallbackSecondaryDumpData</i>例程非常受限于它可以执行的操作。 有关详细信息，请参阅 [Bug 检查回调例程限制](#bug-check-callback-routine-restrictions)。

## <a name="implementing-a-kbcallbacktriagedumpdata-callback-routine"></a>实现 KbCallbackTriageDumpData 回调例程

从 Windows 10 版本1809和 Windows Server 2019 开始，内核模式驱动程序可以实现 *KbCallbackTriageDumpData* 类型的 [*KBUGCHECK_REASON_CALLBACK_ROUTINE*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kbugcheck_reason_callback_routine)回调函数，将虚拟内存范围添加到划分小型转储文件。 系统将在 <i>ReasonSpecificData</i> 参数中传递一个指向描述转储数据的 [**KBUGCHECK_TRIAGE_DUMP_DATA**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_kbugcheck_triage_dump_data) 结构的指针。

在下面的示例中，驱动程序配置会审转储数组，然后注册回调的最小实现：

```cpp
// Globals 
 
KBUGCHECK_REASON_CALLBACK_RECORD ExampleBugcheckCallbackRecord; 
PKTRIAGE_DUMP_DATA_ARRAY gTriageDumpDataArray; 
 
//  call this register function from DriverInit, etc.
 
VOID ExampleRegisterTriageDataCallbacks() 
{ 
 
    // 
    // Allocate a triage dump array in the non-paged pool. 
    // 
 
gTriageDumpDataArray = 
    (PKTRIAGE_DUMP_DATA_ARRAY)ExAllocatePoolWithTag(NonPagedPoolNx, 2*PAGE_SIZE, "Xmpl"); 
 
    // 
    // Initialize the dump data block array. 
    // 
 
    KeInitializeTriageDumpDataArray( gTriageDumpDataArray, 2*PAGE_SIZE, "Example"); 
 
    KeInitializeCallbackRecord( &ExampleBugcheckCallbackRecord ); 
 
    KeRegisterBugCheckReasonCallback( 
        &ExampleBugCheckCallbackRecord, 
        ExampleBugCheckCallbackRoutine, 
        KbCallbackTriageDumpData, 
        "Example" 
        ); 
} 
 
// Callback function 
 
VOID 
ExampleBugCheckCallbackRoutine( 
    KBUGCHECK_CALLBACK_REASON Reason, 
    PKBUGCHECK_REASON_CALLBACK_RECORD Record, 
    PVOID Data, 
    ULONG Length 
    ) 
{ 
    PKBUGCHECK_TRIAGE_DUMP_DATA DumpData; 
    NTSTATUS Status; 
 
    DumpData = (PKBUGCHECK_TRIAGE_DUMP_DATA) Data; 
 
    Status = KeAddTriageDumpDataBlock(gTriageDumpDataArray, gImportant, SizeofGImportant); 
 
    // Pass our arrays back 
 
    if (NT_SUCCESS(Status)) { 
        DumpData->RequiredDataArray = gTriageDumpDataArray; 
    } 
 
    return; 
}
```
<i>KbCallbackTriageDumpData</i>例程非常受限于它可以执行的操作。 有关详细信息，请参阅 [Bug 检查回调例程限制](#bug-check-callback-routine-restrictions)。
