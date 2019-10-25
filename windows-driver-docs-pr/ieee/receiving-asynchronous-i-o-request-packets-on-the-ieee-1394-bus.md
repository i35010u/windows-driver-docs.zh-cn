---
title: 在 IEEE 1394 总线上接收异步 I/O 请求数据包
description: 计算机本身是 IEEE 1394 总线上的一个节点，因此可以接收异步 i/o 请求。
ms.assetid: 7b8eaf40-7fdc-4c25-86a7-8377d2d51877
keywords:
- 接收异步 i/o 请求
- 分配地址范围
- 解决 WDK IEEE 1394 总线
- 后备存储 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 020784e1aa5f377a41dd2774aa8d610fb7a52afd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841531"
---
# <a name="receiving-asynchronous-io-request-packets-on-the-ieee-1394-bus"></a>在 IEEE 1394 总线上接收异步 I/O 请求数据包

计算机本身是 IEEE 1394 总线上的一个节点，因此可以接收异步 i/o 请求。 驱动程序可以通过提交请求\_向总线驱动程序分配\_地址\_范围请求，来分配计算机的 IEEE 1394 地址空间内的地址范围并接收来自外部节点的请求。

当驱动程序分配地址范围时，它可以通过指定一个或多个访问\_标志来指定设备可以发送到分配的地址的事务类型，\_类型\_读取、访问\_标志\_类型\_在请求的 IRB 的**fulAccessType**成员中写入或访问\_标志，\_类型\_锁定。 不是指定类型之一的请求将自动失败。

两个不同的驱动程序可以分配相同的地址范围。 默认情况下，总线驱动程序会自动 demultiplexes 请求，驱动程序只会看到来自驱动程序设备的分配的地址上的请求。 驱动程序可以通过在**AllocateAddressRange. fulAccessType**中指定访问\_标志\_类型\_广播标志来请求接收总线上的所有节点发送到该地址的所有数据包。

* [分配的地址](#allocated-addresses)
* [分配和后备存储](#allocation-and-backing-store)
* [用于接收异步 i/o 请求的客户端驱动程序通知例程](#client-drivers-notification-routine-for-receive-asynchronous-io-requests)
* [提前通知案例中的异步接收](#asynchronous-receive-in-the-pre-notification-case)

## <a name="allocated-addresses"></a>分配的地址

总线驱动程序支持两种不同的策略来分配地址范围。 如果驱动程序需要从硬编码地址开始的特定范围的地址，则它可以在请求的 IRB 的**Required1394Offset**成员中指定硬编码地址，并在 u 中指定地址范围的长度。 **AllocateAddressRange. nLength**。 总线驱动程序将允许两个不同的驱动程序分配相同的地址两次。 如果同一驱动程序尝试从同一地址开始分配两次地址范围，则总线驱动程序将返回状态代码为 "状态"\_"请求"，但会忽略请求本身。

否则，驱动程序可以允许总线驱动程序选择分配的地址。 总线驱动程序跟踪驱动程序分配的所有地址范围，并将仅返回以前未分配的地址。

总线驱动程序不连续分配地址。 地址根据作为后备存储提供的 MDL 进行分段。 MDL 中的每个段对应于地址范围中的一个段。 需要将分配的地址配置为连续的驱动程序可以从非分页池分配连续内存。

如果驱动程序需要保证每个段都小于特定大小，则可以在**AllocateAddressRange. MaxSegmentSize**中指定该大小。 无需将最大段大小设置为**AllocateAddressRange. MaxSegmentSize**的驱动程序设置为零。

总线驱动程序返回 IRB 的**AllocateAddressRange. p1394AddressRange**成员指向的内存位置中的地址范围。 设备驱动程序必须分配一个足够大的数组，以容纳\_范围结构的每个地址，即使在最差的案例分段方案中也是如此。 如果驱动程序未指定段大小，或者其最大段大小大于页\_大小，则驱动程序可以通过使用地址\_和\_大小\_到\_跨页宏来确定最坏情况用于后备存储的缓冲区。 如果最大段大小小于页\_大小，则驱动程序必须分配大小为**AllocateAddressRange. nLength**的数组/**AllocateAddressRange。 MaxSegmentSize** + 2。

当总线驱动程序返回分配的地址时，它将记录在**AllocateAddressRange. hAddressRange**中分配的地址范围的实际数量。

## <a name="allocation-and-backing-store"></a>分配和后备存储

总线驱动程序代表驱动程序接收所有异步数据包请求。 在驱动程序的 behest，它可以透明地处理请求，或者可以将请求调度到驱动程序。 通过在分配地址时设置选项，驱动程序可以选择总线驱动程序处理每个请求的方式。

1. 驱动程序为地址范围提供后备存储，而总线驱动程序通过使用后备存储以透明方式处理所有读取、写入和锁定请求。

    当驱动程序分配地址时，它可以在**AllocateAddressRange**中提供 mdl 来充当后备存储。 总线驱动程序将 MDL 映射到它为驱动程序分配的地址范围，并通过读取或写入 MDL 来处理所有请求。 如果主机控制器支持此方法，则该事务将由主机控制器的 DMA 硬件完全处理。 如果可能，设备驱动程序应该允许总线驱动程序选择分配的地址范围：总线驱动程序将选择支持每个事务的自动 DMA 的1394地址。

    驱动程序必须为**AllocateAddressRange**指定通知\_标志\_从不。

    下面是一个示例：

    ```cpp
    pIRB->u.AllocateAddressRange.Mdl = an MDL previously allocated by the driver.
    pIRB->u.AllocateAddressRange.fulNotificationOptions = NOTIFY_FLAGS_NEVER
    ```

    对于此选项，驱动程序还可以在引发 IRQL 时分配地址范围。 驱动程序可以通过调用端口驱动程序的物理映射例程，直接向端口驱动程序提交请求，绕过通常的 IRP 通信方法。 设备驱动程序将 IRB 传递到端口驱动程序的物理映射例程。 然后，端口驱动程序将异步分配地址范围;端口驱动程序完成后，它将调用设备驱动程序的通知例程，并传入**AllocateAddressRange**，并将**AllocateAddressRange**作为参数传递。 通知例程是在调度\_级别调用的。

    设备驱动程序**可以通过将**GET\_本地\_主机\_信息请求提交到总线驱动程序\_\_，将 GET 本地主机信息请求提交到端口驱动程序的物理映射例程。 总线驱动程序将返回一个 GET\_本地\_主机\_信息4结构，该结构包含物理映射例程，还会返回一个上下文参数，其中的设备驱动程序与 IRB 一起传递到物理映射例程。

    下面的示例演示了驱动程序如何设置物理映射例程的请求。 物理映射例程不会更改，因此驱动程序通常只提交此请求一次。

    ```cpp
    GET_LOCAL_HOST_INFO5 PhysMapInfo;
    pGetInfoIRB->FunctionNumber = GET_LOCAL_HOST_INFO;
    pGetInfoIRB->GET_PHYS_ADDR_ROUTINE;

    /* Driver submits the request. */
    ```

    继续此示例，该驱动程序可以如何使用物理映射例程以提升的 IRQL 提交请求。

    ```cpp
    VOID AllocationCompletionRoutine(PVOID Context);
    /* Driver fills out the members of the IRB, including these: */
    pIRB->u.AllocateAddressRange.Mdl = an MDL previously allocated by the driver.
    pIRB->u.AllocateAddressRange.fulNotificationOptions = NOTIFY_FLAGS_NEVER
    pIRB->Callback = AllocationCompletionRoutine;
    pIRB->Context = information specific to this allocation the driver wants passed to its callback.

    /* Driver submits the request to the physical mapping routine. */
    PhysMapInfo.PhysAddrMappingRoutine(PhysMapInfo.Context, pIRB);

    /*
    The bus driver does the allocation asynchronously. When it's done, it will signal the driver by executing AllocationCompletionRoutine(pIRB->u.AllocateAddressRange.Context);
    */
    ```

2. 驱动程序为地址范围提供后备存储。 总线驱动程序完成每个 i/o 事务后，会通知驱动程序。

    驱动程序可以提供单个 MDL 或 MDLs 的链接列表作为后备存储。 如果驱动程序提供了单个 MDL，则总线驱动程序会将数据泵移入或移出 MDL，以响应异步请求。 完成事务后，它会通过调用驱动程序提供的通知回调来发出设备驱动程序的信号。

    设备驱动程序在 IRB 的**AllocateAddressRange**成员中提供通知例程。 驱动程序必须在\_XXX 标志后至少设置一个通知\_标志\_。 当总线驱动程序调用例程时，它将传递一条通知\_信息结构，该结构指定 mdl 后备存储（在**mdl**中）、事务开始的 mdl 中的字节偏移量（在**ulOffset**中）以及范围的长度（以字节为单位）受影响的地址（在**nLength**中）。 通知例程是在调度\_级别调用的。 该驱动程序在**AllocateAddressRange**中传递的此请求的任何上下文信息都通过通知\_信息的**上下文**成员中的总线驱动程序传递。

    仅使用一个 MDL，存在同步问题的风险：设备写入地址范围的速度可能比驱动程序可以读取的速度更快。 若要避免此类冲突，对于设备仅具有写入访问权限的地址，驱动程序可以在**FifoSListHead**中提供 MDLs 的链接列表，并在**AllocateAddressRange**中提供自旋锁。 当总线驱动程序收到每个异步请求数据包时，它将保留自旋锁，并弹出列表中的第一个元素来完成请求。 然后，它调用驱动程序的通知例程。

    在通知\_的信息结构中，总线驱动程序提供它用于处理事务的 MDL （在**MDL**中）、受影响的第一个地址的字节偏移量（在**ulOffset**中）以及受影响的地址范围的长度（以**nLength**）。 它还提供 MDL\_FIFO 的地址（在**fifo**中）。 在从其通知例程返回驱动程序之前，应使用**Fifo**将元素推送回列表中，或者提供相同大小的其他 MDL;否则，总线驱动程序将用完了 MDLs 来处理来自设备的写入请求。

    下面是使用此类型通知的扩展示例。 全局驱动程序会创建一个互锁、单向链接列表和一个旋转锁。 驱动程序需要在引发的 IRQLs 访问链接列表和旋转锁定，因此它们必须位于非分页内存中。 通常，驱动程序会将它们保留在其设备扩展中。

    ```cpp
    PSLIST_HEADER FifoSListHead;
    KSPIN_LOCK FifoSpinLock;

    ExInitializeSListHead(FifoSListHead);
    KeInitializeSpinLock(FifoSpinLock);
    ```

    当驱动程序提交请求时，它可以设置相关的 IRB 成员，如下所示：

    ```cpp
    VOID DriverNotificationRoutine(PNOTIFICATION_INFO NotificationInfo);

    pIRB->u.AllocateAddressRange.Mdl = NULL;
    pIRB->u.AllocateAddressRange.fulAccessType = ACCESS_FLAGS_READ;
    pIRB->u.AllocateAddressRange.fulNotificationOptions = NOTIFY_FLAGS_AFTER_WRITE;
    pIRB->u.AllocateAddressRange.FifoSListHead = FifoSListHead;
    pIRB->u.AllocateAddressRange.FifoSpinLock = FifoSpinLock;
    pIRB->u.AllocateAddressRange.Callback = DriverNotificationRoutine;
    pIRB->u.AllocateAddressRange.Context = context information specific to this request -- the bus driver will pass this as the Context member of the NOTIFICATION_INFO it passes to NotificationRoutine.
    ```

    在回调中，驱动程序需要分配新的 MDL 并将其推送到列表，或将原始 MDL 推回列表。 对于后一种情况，总线驱动程序为当前 MDL 传递\_FIFO 的原始地址。 下面是在列表中推送当前 MDL 的驱动程序示例：

    ```cpp
    ExInterlockedPushEntrySList(FifoSListHead, NotificationInfo->Fifo->FifoList, FifoSpinLock);
    ```

    如果驱动程序将单个 MDL 指定为原始分配请求中的后备存储，则驱动程序可能返回一个或多个地址范围。

3. 总线驱动程序会在每次请求到达时发出驱动程序信号，并将数据包交给驱动程序。

    驱动程序在 IRB 的**AllocateAddressRange**成员中提供回调。 忽略\_XXX 标志后发出\_标志\_，并将所有数据包传递给驱动程序以进行处理。

    驱动程序必须将**AllocateAddressRange**的**Mdl**、 **FifoSListHead**和**FifoSpinLock**成员设置为**NULL**。 下面是一个驱动程序设置的示例，该驱动程序希望在收到所有三个类型的异步请求数据包时收到通知。

    ```cpp
    VOID DriverNotificationRoutine( IN PNOTIFICATION_INFO NotificationInfo );

    pIRB->u.AllocateAddressRange.Callback = DriverNotificationRoutine;
    pIRB->u.AllocateAddressRange.Context = information specific to this address range.
    pIRB->u.AllocateAddressRange.Mdl = NULL;
    pIRB->u.AllocateAddressRange.FifoSListHead = NULL;
    pIRB->u.AllocateAddressRange.FifoSpinLock = NULL;
    ```

    总线驱动程序分配一个连续的地址范围。

    总线驱动程序将通知\_信息结构传递给驱动程序的回调例程。 设备驱动程序必须创建其自己的响应数据包（有关详细信息，请参阅 IEEE 1394 规范），并且它必须分配其自己的缓冲区以包含它创建的响应数据包。 响应数据包必须来自非分页池或已探测和锁定的缓冲区。

    在通知\_信息中，总线驱动程序在**ResponseMdl**成员中提供了未初始化的 MDL。 它还提供指向内存位置的指针，该内存位置要求设备驱动程序输入指向响应数据包的指针（在**ResponsePacket**中）和响应数据包长度（在**ResponseLength**中）。 驱动程序还可以提供内核事件对象。 总线驱动程序在完成事务后发出内核事件对象信号。

    下面的示例演示了设备驱动程序如何在其通知例程中填写所需的信息。

    ```cpp
    /* Suppose the driver creates its response packet in PVOID ResponsePacket, of length ResponseLength. It has created a kernel event ResponseEvent. */
    MmInitializeMdl(NotificationInfo->ResponseMdl, ResponsePacket, ResponseLength);
    MmBuildMdlFForNonPagedPool(Notification->ResponseMdl);
    *(NotificationInfo->ResponsePacket) = ResponsePacket.
    *(NotificationInfo->ResponseLength) = ResponseLength;
    *(NotificationInfo)->ResponseEvent = Event;
    ```

## <a name="client-drivers-notification-routine-for-receive-asynchronous-io-requests"></a>用于接收异步 i/o 请求的客户端驱动程序通知例程

客户端驱动程序必须在驱动程序的异步接收通知例程中执行以下任务：

* 验证传递给客户端驱动程序的[**通知\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)结构的成员。
* 若要成功读取/锁定请求（在其中通过响应数据包返回数据），客户端驱动程序必须：
  * 为响应数据包数据调用[**WdfMemoryCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate) （基于 WDM 的客户端驱动程序的[**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) ）来分配内存。
  * 用要返回的数据填充该缓冲区。
  * 初始化**ResponseMdl**成员并引用缓冲区。 可以调用[**MmInitializeMdl**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)和[**MmBuildMdlForNonPagedPool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool)。
  * 将 **\*NotificationInfo-&gt;ResponsePacket**设置为指向缓冲区。
  * 将 **\*NotificationInfo-&gt;ResponseLength**设置为返回的响应数据的大小，即 quadlet 读取请求的4。
  * 为响应事件调用[**WdfMemoryCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate) （基于 WDM 的客户端驱动程序的[**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) ）来分配内存。
  * 将 **\*NotificationInfo-&gt;ResponseEvent**设置为指向事件缓冲区。
  * 计划要等待事件的工作项，并在响应事件发出信号后释放响应数据包和事件数据缓冲区。
  * 将**NotificationInfo-&gt;ResponseCode**设置为 RCODE\_完成\_。

## <a name="asynchronous-receive-in-the-pre-notification-case"></a>提前通知案例中的异步接收

旧版1394总线驱动程序无法使用预先通知机制完成异步接收事务。 有关详细信息，请参阅[知识库：不使用预先通知（2635883）发送的 IEEE 1394 异步接收响应](https://support.microsoft.com/help/2635883/ieee-1394-async-receive-response-not-sent-using-pre-notification)。

对于新的1394总线驱动程序，预通知事例中的客户端驱动程序通知回调例程的预期行为如下所示：

* 如果[**通知\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)结构的**Mdl**和**Fifo**成员为 NULL，则执行预先通知。
* [ **\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)结构的通知的**ResponseMdl**、 **ResponsePacket**、 **RESPONSELENGTH**和**ResponseEvent**成员不能为 NULL。
* [ **\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)结构的通知的**fulNotificationOptions**成员必须指示触发通知的操作（读取、写入、锁定）。 只有一个标志（通知\_标志在\_读取后\_，在\_写入后通知\_标志\_，或在每次调用通知例程时通知\_标志\_。
* 可以通过检查异步\_包结构的**RequestPacket-&gt;AP\_tCode**成员来识别请求的类型。 成员指示指定请求类型的 TCODE，例如 block 或 quadlet 读/写，即锁请求的类型。 在 1394 .h 中声明 ASYNC\_数据包结构。
* [**通知\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)的**ResponsePacket**和**ResponseEvent**成员包含指向指针的指针。 因此，你必须相应地引用指向响应数据包和响应事件的指针。
* [**通知\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)的**ResponseLength**成员是指向 ULONG 变量的指针。 因此，当为请求（例如 for read & 锁请求）设置响应数据长度时，必须适当地取消对成员的引用。
* 1394客户端驱动程序负责为响应数据包和响应事件（来自非分页池）分配内存，并在传递响应后释放该内存。 建议将工作项排队，并且工作项应等待响应事件。 此事件由1394总线驱动程序在发送响应后发出信号。 然后，客户端驱动程序可以释放工作项中的内存。
* [**通知\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)结构中的**ResponseCode**成员必须设置为在 RCODE 中定义的值之一。 如果**ResponseCode**设置为 RCODE 以外的任何值\_响应\_完成，1394总线驱动程序将发送错误响应数据包。 对于读取或锁定请求，请求不会返回任何数据。 在 Windows 7 中，可能会泄漏内存，有关详细信息，请参阅[知识库： IEEE 1394 总线驱动程序中执行异步通知回调的内存泄漏（2023232）](https://support.microsoft.com/help/2023232)。
* 对于读取和锁定请求， [ **\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)结构的通知的**ResponsePacket**成员必须指向要在异步响应数据包中返回的数据。

下面的代码示例显示了工作项实现和客户端驱动程序的通知例程。

```cpp
VOID
kmdf1394_NotifyRoutineWorkItem (
                                 IN WDFWORKITEM  WorkItem)
{
    NTSTATUS                 ntStatus;
    PNOTIFY_WORKITEM_CONTEXT notifyContext = GetNotifyWorkitemContext(WorkItem);

    Enter();

    ASSERT(notifyContext);

    ntStatus = KeWaitForSingleObject(
                                     &notifyContext->responseEvent,
                                     Executive,
                                     KernelMode,
                                     FALSE,
                                     NULL);
    if (!NT_SUCCESS(ntStatus))
    {
        DoTraceLevelMessage(TRACE_LEVEL_ERROR,
                            TRACE_FLAG_ASYNC,
                            "Wait on notify response event failed: %!STATUS!\n",
                            ntStatus);
    }

    WdfObjectDelete (WorkItem);

    Exit();
}

VOID
kmdf1394_NotificationCallback (
    IN PNOTIFICATION_INFO   NotifyInfo)
{
    PASYNC_PACKET           asyncPacket = (PASYNC_PACKET)NotifyInfo->RequestPacket;
    PASYNC_ADDRESS_DATA     asyncAddressData = NotifyInfo->Context;
    PULONG                  responseQuadlet;
    WDF_WORKITEM_CONFIG     workItemConfig;
    WDFWORKITEM             workItem;
    WDF_OBJECT_ATTRIBUTES   attributes;
    PNOTIFY_WORKITEM_CONTEXT notifyContext;
    NTSTATUS                ntStatus;

    Enter();

    DoTraceLevelMessage(TRACE_LEVEL_INFORMATION,
                        TRACE_FLAG_ASYNC,
                        "NotifyInfo Mdl %p ulOffset %08x nLength %08x fulNotificationOptions %08x Context %p RCode %x Pkt %p\n",
                        NotifyInfo->Mdl,
                        NotifyInfo->ulOffset,
                        NotifyInfo->nLength,
                        NotifyInfo->fulNotificationOptions,
                        NotifyInfo->Context,
                        NotifyInfo->ResponseCode,
                        asyncPacket);

    if (NotifyInfo->Mdl)
    {
        // Post-Notification
        switch (NotifyInfo->fulNotificationOptions)
        {
            case NOTIFY_FLAGS_AFTER_LOCK:
                NotifyInfo->ResponseCode = RCODE_TYPE_ERROR;
                break;

            case NOTIFY_FLAGS_AFTER_WRITE:
                NotifyInfo->ResponseCode = RCODE_TYPE_ERROR;
                break;

            case NOTIFY_FLAGS_AFTER_READ:
                // Don't touch ResponseCode if no error
                // NotifyInfo->ResponseCode = RCODE_RESPONSE_COMPLETE;
                break;

            default:
                NotifyInfo->ResponseCode = RCODE_TYPE_ERROR;
                break;
        }
    }
    else
    {
        // Pre-Notification
        if (asyncPacket)
        {
            if ( !NotifyInfo->ResponseMdl ||
                    !NotifyInfo->ResponsePacket ||
                    !NotifyInfo->ResponseLength ||
                    !NotifyInfo->ResponseEvent )
            {
                DoTraceLevelMessage(TRACE_LEVEL_ERROR,
                                    TRACE_FLAG_ASYNC,
                                    "Pre-Notification failure: missing Response field(s)!\n");
                DoTraceLevelMessage(TRACE_LEVEL_ERROR,
                                    TRACE_FLAG_ASYNC,
                                    "ResponseMdl %p\tResponsePacket %p\tResponseLength %p\tResponseEvent %p\n",
                                    NotifyInfo->ResponseMdl, NotifyInfo->ResponsePacket,
                                    NotifyInfo->ResponseLength, NotifyInfo->ResponseEvent);
                if (NotifyInfo->ResponsePacket != NULL)
                {
                    DoTraceLevelMessage(TRACE_LEVEL_ERROR,
                                        TRACE_FLAG_ASYNC,
                                        "\t*ResponsePacket %p\n",
                                        *NotifyInfo->ResponsePacket);
                }
                NotifyInfo->ResponseCode = RCODE_TYPE_ERROR;
            }
            else if ( NULL == asyncAddressData )
            {
                DoTraceLevelMessage(TRACE_LEVEL_ERROR,
                                    TRACE_FLAG_ASYNC,
                                    "Pre-Notification failure: missing Notify Context!\n");
                NotifyInfo->ResponseCode = RCODE_TYPE_ERROR;
            }
            else
            {
                DoTraceLevelMessage(TRACE_LEVEL_INFORMATION,
                                    TRACE_FLAG_ASYNC,
                                    "AddrData %p DevExt %p Buffer %p Len %x hAddrRange %!HANDLE! Mdl %p\n",
                                    asyncAddressData,
                                    asyncAddressData->DeviceExtension,
                                    asyncAddressData->Buffer,
                                    asyncAddressData->nLength,
                                    asyncAddressData->hAddressRange,
                                    asyncAddressData->pMdl);

                switch (asyncPacket->AP_tCode)
                {
                    case TCODE_LOCK_REQUEST:
                        NotifyInfo->ResponseCode = RCODE_TYPE_ERROR;
                        break;

                    case TCODE_WRITE_REQUEST_QUADLET:
                    case TCODE_WRITE_REQUEST_BLOCK:
                        NotifyInfo->ResponseCode = RCODE_TYPE_ERROR;
                        break;

                    case TCODE_READ_REQUEST_BLOCK:
                        NotifyInfo->ResponseCode = RCODE_DATA_ERROR;
                        break;

                    case TCODE_READ_REQUEST_QUADLET:
                        // only implementing Quadlet Read for now

                        // Create a WdfWorkItem, with notifyResponse as its context,
                        // to handle waiting for the Response Event & cleaning up all the response stuff

                        WDF_WORKITEM_CONFIG_INIT (&workItemConfig, kmdf1394_NotifyRoutineWorkItem);

                        WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&attributes, NOTIFY_WORKITEM_CONTEXT);

                        attributes.ParentObject = WdfObjectContextGetObject(asyncAddressData->DeviceExtension);

                        ntStatus = WdfWorkItemCreate( &workItemConfig,
                            &attributes,
                            &workItem);

                        if (!NT_SUCCESS (ntStatus))
                        {
                            DoTraceLevelMessage(TRACE_LEVEL_ERROR,
                                                TRACE_FLAG_ASYNC,
                                                "Failed to create workitem %x\n",
                                                ntStatus);

                            NotifyInfo->ResponseCode = RCODE_DATA_ERROR;
                            break;
                        }

                        notifyContext = GetNotifyWorkitemContext(workItem);

                        notifyContext->asyncAddressData = asyncAddressData;

                        // NotifyInfo->ResponsePacket
                        // memory location that the driver fills in with
                        // a pointer to the beginning of its response packet

                        // parent this memory object to the workitem so both can be cleaned up together
                        WDF_OBJECT_ATTRIBUTES_INIT (&attributes);
                        attributes.ParentObject = workItem;

                        ntStatus = WdfMemoryCreate(
                                                   &attributes,
                                                   NonPagedPool,
                                                   POOLTAG_KMDF_VDEV,
                                                   sizeof(ULONG),
                                                   &notifyContext->responseMemory,
                                                   &responseQuadlet);

                        if (!NT_SUCCESS(ntStatus) || !responseQuadlet)
                        {
                            DoTraceLevelMessage(TRACE_LEVEL_ERROR,
                                                TRACE_FLAG_ASYNC,
                                                "Failed to allocate Response Data Memory: %!STATUS!\n",
                                                ntStatus);

                            WdfObjectDelete (workItem);

                            NotifyInfo->ResponseCode = RCODE_DATA_ERROR;
                            break;
                        }

                        RtlFillMemory(responseQuadlet, sizeof(ULONG), 0x8F);    // dummy data for testing

                        // NotifyInfo->ResponseMdl
                        // initialize MDL for a nonpageable buffer,
                        // and fill the buffer with the response packet
                        MmInitializeMdl(NotifyInfo->ResponseMdl,
                                        responseQuadlet,
                                        sizeof(ULONG));
                        MmBuildMdlForNonPagedPool(NotifyInfo->ResponseMdl);

                        // do what it looks like the New (KMDF) stack expects,
                        // which is that NotifyInfo->ResponsePacket points to the
                        // data following the Async Packet header
                        *NotifyInfo->ResponsePacket = (PVOID)&responseQuadlet;

                        // NotifyInfo->ResponseEvent
                        // memory location that the driver fills in with
                        // the kernel event the bus driver should use to signal
                        // that it has completed sending the response packet
                        KeInitializeEvent(&notifyContext->responseEvent, NotificationEvent, FALSE);

                        *NotifyInfo->ResponseEvent = &notifyContext->responseEvent;

                        // NotifyInfo->ResponseLength
                        // memory location that the driver fills in with
                        // the length of its response packet
                        *NotifyInfo->ResponseLength = sizeof(ULONG);

                        // NotifyInfo->ResponseCode
                        // specifies the result of the driver's response to the request
                        NotifyInfo->ResponseCode = RCODE_RESPONSE_COMPLETE;

                        // Enqueue the work item to clean up after notification completion
                        WdfWorkItemEnqueue (workItem);

                        DoTraceLevelMessage(TRACE_LEVEL_INFORMATION,
                                            TRACE_FLAG_ASYNC,
                                            "Pre-Notification: Read Quadlet: Notify Response Handle %!HANDLE! Data %08x Event %p\n",
                                            notifyContext->responseMemory,
                                            *responseQuadlet,
                                            &notifyContext->responseEvent);

                        break;

                    default:
                        NotifyInfo->ResponseCode = RCODE_TYPE_ERROR;
                        break;
                } // switch (asyncPacket->AP_tCode)
            } // else [pre-notification params OK]
        } // if (asyncPacket)
        else
        {
            DoTraceLevelMessage(TRACE_LEVEL_ERROR,
                                TRACE_FLAG_ASYNC,
                                "Pre-Notification failure: no RequestPacket!\n");
            NotifyInfo->ResponseCode = RCODE_DATA_ERROR;
        }
    }

    ExitS( NotifyInfo->ResponseCode | RCODE_STATUS_MASK );
    return;
} // kmdf1394_NotificationCallback
```
