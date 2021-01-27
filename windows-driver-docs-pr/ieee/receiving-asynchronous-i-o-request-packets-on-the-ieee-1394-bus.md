---
title: 在 IEEE 1394 总线上接收异步 I/O 请求数据包
description: 计算机本身是 IEEE 1394 总线上的一个节点，因此可以接收异步 i/o 请求。
keywords:
- 接收异步 i/o 请求
- 分配地址范围
- 解决 WDK IEEE 1394 总线
- 后备存储 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7e14fac4fde8cbdfc5af644bf15f12dcc516493
ms.sourcegitcommit: 5e51e63585f35597cf06fc0ab5c0cc7cb39ca22a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "98861861"
---
# <a name="receiving-asynchronous-io-request-packets-on-the-ieee-1394-bus"></a>在 IEEE 1394 总线上接收异步 I/O 请求数据包

计算机本身是 IEEE 1394 总线上的一个节点，因此可以接收异步 i/o 请求。 驱动程序可以通过将请求 \_ 分配 \_ 地址 \_ 范围请求提交到总线驱动程序来分配计算机的 IEEE 1394 地址空间中的地址范围，并接收来自外部节点的请求。

当驱动程序分配地址范围时，它可以通过 \_ \_ \_ \_ \_ \_ \_ \_ \_ 在请求的 IRB 的 **fulAccessType** 成员中指定一个或多个访问标志类型 "读取"、"访问标志类型写入" 或 "访问标志类型锁定" 来指定设备可以发送到分配的地址的事务类型。 不是指定类型之一的请求将自动失败。

两个不同的驱动程序可以分配相同的地址范围。 默认情况下，总线驱动程序会自动 demultiplexes 请求，驱动程序只会看到来自驱动程序设备的分配的地址上的请求。 驱动程序可以通过 \_ \_ \_ 在 **fulAccessType** 中指定访问标志类型广播标志，请求它们接收所有由总线上的节点发送到地址的数据包。

* [分配的地址](#allocated-addresses)
* [分配和后备存储](#allocation-and-backing-store)
* [用于接收异步 i/o 请求的客户端驱动程序通知例程](#client-drivers-notification-routine-for-receive-asynchronous-io-requests)
* [提前通知案例中的异步接收](#asynchronous-receive-in-the-pre-notification-case)

## <a name="allocated-addresses"></a>分配的地址

总线驱动程序支持两种不同的策略来分配地址范围。 如果驱动程序需要从硬编码地址开始的特定范围的地址，则它可以在请求的 IRB 的 Required1394Offset 成员中指定硬编码地址，并指定 **AllocateAddressRange** 中地址范围的 **长度。** 总线驱动程序将允许两个不同的驱动程序分配相同的地址两次。 如果同一驱动程序尝试分配的地址范围从同一地址开始两次，则总线驱动程序将返回状态代码为 "成功" 的请求 \_ ，但会忽略请求本身。

否则，驱动程序可以允许总线驱动程序选择分配的地址。 总线驱动程序跟踪驱动程序分配的所有地址范围，并将仅返回以前未分配的地址。

总线驱动程序不连续分配地址。 地址根据作为后备存储提供的 MDL 进行分段。 MDL 中的每个段对应于地址范围中的一个段。 需要将分配的地址配置为连续的驱动程序可以从非分页池分配连续内存。

如果驱动程序需要保证每个段都小于特定大小，则可以在 **AllocateAddressRange. MaxSegmentSize** 中指定该大小。 无需将最大段大小设置为 **AllocateAddressRange. MaxSegmentSize** 的驱动程序设置为零。

总线驱动程序返回 IRB 的 **AllocateAddressRange. p1394AddressRange** 成员指向的内存位置中的地址范围。 设备驱动程序必须分配一个足够大的数组，以便保存每个地址 \_ 范围结构，甚至在最差的案例分段方案中也是如此。 如果驱动程序未指定段大小，或者其最大段大小超过页面 \_ 大小，则驱动程序可以通过使用用于 \_ \_ \_ \_ \_ 后备存储的缓冲区上的地址和大小来跨页面宏来确定最坏的情况。 如果最大段大小小于页面 \_ 大小，则驱动程序必须分配大小为 **AllocateAddressRange** /  + 2 的数组。

当总线驱动程序返回分配的地址时，它将记录在 **AllocateAddressRange. hAddressRange** 中分配的地址范围的实际数量。

## <a name="allocation-and-backing-store"></a>分配和后备存储

总线驱动程序代表驱动程序接收所有异步数据包请求。 在驱动程序的 behest，它可以透明地处理请求，或者可以将请求调度到驱动程序。 通过在分配地址时设置选项，驱动程序可以选择总线驱动程序处理每个请求的方式。

1. 驱动程序为地址范围提供后备存储，而总线驱动程序通过使用后备存储以透明方式处理所有读取、写入和锁定请求。

    当驱动程序分配地址时，它可以在 **AllocateAddressRange** 中提供 mdl 来充当后备存储。 总线驱动程序将 MDL 映射到它为驱动程序分配的地址范围，并通过读取或写入 MDL 来处理所有请求。 如果主机控制器支持此方法，则该事务将由主机控制器的 DMA 硬件完全处理。 如果可能，设备驱动程序应该允许总线驱动程序选择分配的地址范围：总线驱动程序将选择支持每个事务的自动 DMA 的1394地址。

    驱动程序必须 \_ \_ 为 **AllocateAddressRange** 指定通知标志从不。

    下面是一个示例：

    ```cpp
    pIRB->u.AllocateAddressRange.Mdl = an MDL previously allocated by the driver.
    pIRB->u.AllocateAddressRange.fulNotificationOptions = NOTIFY_FLAGS_NEVER
    ```

    对于此选项，驱动程序还可以在引发 IRQL 时分配地址范围。 驱动程序可以通过调用端口驱动程序的物理映射例程，直接向端口驱动程序提交请求，绕过通常的 IRP 通信方法。 设备驱动程序将 IRB 传递到端口驱动程序的物理映射例程。 然后，端口驱动程序将异步分配地址范围;端口驱动程序完成后，它将调用设备驱动程序的通知例程，并传入 **AllocateAddressRange**，并将 **AllocateAddressRange** 作为参数传递。 通知例程是在调度级别调用的 \_ 。

    设备驱动程序可以通过将 "获取本地主机信息" 请求提交到总线驱动程序，将 "获取本地主机信息" 请求提交到端口驱动程序的物理映射例程 \_ \_ \_ ，其中 **nLevel** = get \_ PHYS \_ ADDR \_ 例程。 总线驱动程序返回一个 \_ "获取本地 \_ 主机 \_ " 信息4结构，其中包含物理映射例程，并返回一个上下文参数，其中的设备驱动程序与 IRB 一起传递到物理映射例程。

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

    设备驱动程序在 IRB 的 **AllocateAddressRange** 成员中提供通知例程。 驱动程序必须在 \_ \_ XXX 标志后至少设置一个通知标志 \_ 。 当总线驱动程序调用例程时，它将传递一条通知 \_ 信息结构，该结构指定 **mdl** 中 (的 mdl 后备存储) 、事务开始)  (的 mdl 中的字节偏移量，以及 **nLength** (中受影响的地址范围的长度（以字节为单位）。 通知例程是在调度级别调用的 \_ 。 该驱动程序在 **AllocateAddressRange** 中传递的此请求的任何上下文信息都由总线驱动程序在通知信息的 **上下文** 成员中传递。 \_

    仅使用一个 MDL，存在同步问题的风险：设备写入地址范围的速度可能比驱动程序可以读取的速度更快。 若要避免此类冲突，对于设备仅具有写入访问权限的地址，驱动程序可以在 **FifoSListHead** 中提供 MDLs 的链接列表，并在 **AllocateAddressRange** 中提供自旋锁。 当总线驱动程序收到每个异步请求数据包时，它将保留自旋锁，并弹出列表中的第一个元素来完成请求。 然后，它调用驱动程序的通知例程。

    在通知 \_ 信息结构中，总线驱动程序提供了用于 (处理 **mdl**) 的 mdl 的 mdl、受影响的第一个地址 (**ulOffset**) 中的字节偏移量，以及 **nLength** (中受影响的地址范围的长度。 它还提供 \_ **fifo**) 中 MDL (的地址 FIFO。 在从其通知例程返回驱动程序之前，应使用 **Fifo** 将元素推送回列表中，或者提供相同大小的其他 MDL;否则，总线驱动程序将用完了 MDLs 来处理来自设备的写入请求。

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

    在回调中，驱动程序需要分配新的 MDL 并将其推送到列表，或将原始 MDL 推回列表。 对于后一种情况，总线驱动程序将传递 \_ 当前 MDL 的原始地址 FIFO。 下面是在列表中推送当前 MDL 的驱动程序示例：

    ```cpp
    ExInterlockedPushEntrySList(FifoSListHead, NotificationInfo->Fifo->FifoList, FifoSpinLock);
    ```

    如果驱动程序将单个 MDL 指定为原始分配请求中的后备存储，则驱动程序可能返回一个或多个地址范围。

3. 总线驱动程序会在每次请求到达时发出驱动程序信号，并将数据包交给驱动程序。

    驱动程序在 IRB 的 **AllocateAddressRange** 成员中提供回调。 \_ \_ 忽略 XXX 标志后的通知标志 \_ ，并将所有数据包移交给驱动程序以进行处理。

    驱动程序必须将 **AllocateAddressRange** 的 **Mdl**、 **FifoSListHead** 和 **FifoSpinLock** 成员设置为 **NULL**。 下面是一个驱动程序设置的示例，该驱动程序希望在收到所有三个类型的异步请求数据包时收到通知。

    ```cpp
    VOID DriverNotificationRoutine( IN PNOTIFICATION_INFO NotificationInfo );

    pIRB->u.AllocateAddressRange.Callback = DriverNotificationRoutine;
    pIRB->u.AllocateAddressRange.Context = information specific to this address range.
    pIRB->u.AllocateAddressRange.Mdl = NULL;
    pIRB->u.AllocateAddressRange.FifoSListHead = NULL;
    pIRB->u.AllocateAddressRange.FifoSpinLock = NULL;
    ```

    总线驱动程序分配一个连续的地址范围。

    总线驱动程序将通知 \_ 信息结构传递给驱动程序的回调例程。 设备驱动程序必须创建其自身的响应数据包 (参阅 IEEE 1394 规范以了解详细信息) ，并且它必须分配其自己的缓冲区才能包含它创建的响应数据包。 响应数据包必须来自非分页池或已探测和锁定的缓冲区。

    在通知 \_ 信息中，总线驱动程序在 **ResponseMdl** 成员中提供未初始化的 MDL。 它还提供指向内存位置的指针，该内存位置要求设备驱动程序输入指向 **ResponsePacket**) 中的响应数据包 (的指针，以及 **ResponseLength**) 中的响应数据包长度 (。 驱动程序还可以提供内核事件对象。 总线驱动程序在完成事务后发出内核事件对象信号。

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

* 验证传递给客户端驱动程序的 [**通知 \_ 信息**](/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k) 结构的成员。
* 若要成功读取/锁定请求 (通过响应数据包) 返回数据的位置，客户端驱动程序必须：
  * 为响应数据包数据调用基于 WDM 的客户端驱动程序) 的 [**WdfMemoryCreate**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate) ([**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) 来分配内存。
  * 用要返回的数据填充该缓冲区。
  * 初始化 **ResponseMdl** 成员并引用缓冲区。 可以调用 [**MmInitializeMdl**](../kernel/mm-bad-pointer.md) 和 [**MmBuildMdlForNonPagedPool**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool)。
  * 将 **\* NotificationInfo- &gt; ResponsePacket** 设置为指向缓冲区。
  * 将 **\* NotificationInfo- &gt; ResponseLength** 设置为返回的响应数据的大小，该大小为4，表示 quadlet 读取请求) 。
  * 为响应事件调用基于 WDM 的客户端驱动程序) 的 [**WdfMemoryCreate**](/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycreate) ([**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) 分配内存。
  * 将 **\* NotificationInfo- &gt; ResponseEvent** 设置为指向事件缓冲区。
  * 计划要等待事件的工作项，并在响应事件发出信号后释放响应数据包和事件数据缓冲区。
  * 将 **NotificationInfo- &gt; ResponseCode** 设置为 RCODE \_ 响应 \_ 完成。

## <a name="asynchronous-receive-in-the-pre-notification-case"></a>提前通知案例中的异步接收

旧版1394总线驱动程序无法使用预先通知机制完成异步接收事务。

对于新的1394总线驱动程序，预通知事例中的客户端驱动程序通知回调例程的预期行为如下所示：

* 如果 [**通知 \_ 信息**](/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)结构的 **Mdl** 和 **Fifo** 成员为 NULL，则执行预先通知。
* [**通知 \_ 信息**](/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)结构的 **ResponseMdl**、 **ResponsePacket**、 **ResponseLength** 和 **ResponseEvent** 成员不得为空。
* [**通知 \_ 信息**](/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)结构的 **fulNotificationOptions** 成员必须指示触发通知 (读取、写入、锁定) 的操作。 只有一个标志 (\_ \_ 在读取后通知标志 \_ ，在写入后通知 \_ 标记 \_ \_ ， \_ 或 \_ 在 \_ 每次调用通知例程时通知) 可以设置通知。
* 可以通过检查异步包结构的 **RequestPacket- &gt; AP \_ tCode** 成员来识别请求的类型 \_ 。 成员指示指定请求类型的 TCODE，例如 block 或 quadlet 读/写，即锁请求的类型。 \_在 1394 .h 中声明异步数据包结构。
* [**通知 \_ 信息**](/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)的 **ResponsePacket** 和 **ResponseEvent** 成员包含指向指针的指针。 因此，你必须相应地引用指向响应数据包和响应事件的指针。
* [**通知 \_ 信息**](/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)的 **RESPONSELENGTH** 成员是指向 ULONG 变量的指针。 因此，在为请求（如）设置响应数据长度时，必须对该成员进行适当的取消引用，如) & 锁请求。
* 1394客户端驱动程序负责为从非分页池)  (的响应数据包和响应事件分配内存，并在传递响应后释放该内存。 建议将工作项排队，并且工作项应等待响应事件。 此事件由1394总线驱动程序在发送响应后发出信号。 然后，客户端驱动程序可以释放工作项中的内存。
* [**通知 \_ 信息**](/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)结构中的 **ResponseCode** 成员必须设置为 RCODE 中定义的其中一个值。 如果 **ResponseCode** 设置为 RCODE \_ 响应完成以外的任何值 \_ ，1394总线驱动程序将发送错误响应数据包。 对于读取或锁定请求，请求不会返回任何数据。
* 对于读取和锁定请求，[**通知 \_ 信息**](/windows-hardware/drivers/ddi/1394/ns-1394-_notification_info_w2k)结构的 **ResponsePacket** 成员必须指向要在异步响应数据包中返回的数据。

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
