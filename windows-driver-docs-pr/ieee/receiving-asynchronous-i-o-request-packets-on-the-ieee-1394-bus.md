---
title: 在 IEEE 1394 总线上接收异步 I/O 请求数据包
description: 计算机本身的节点上的 IEEE 1394 总线，并因此可接收异步 I/O 请求。
ms.assetid: 7b8eaf40-7fdc-4c25-86a7-8377d2d51877
keywords:
- 接收异步 I/O 请求
- 分配地址范围
- 解决了 WDK IEEE 1394 总线
- 后备存储 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a84e476e93898e7ab2a6bb27aabb411baea3c6ef
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349660"
---
# <a name="receiving-asynchronous-io-request-packets-on-the-ieee-1394-bus"></a>在 IEEE 1394 总线上接收异步 I/O 请求数据包


计算机本身的节点上的 IEEE 1394 总线，并因此可接收异步 I/O 请求。 驱动程序可以分配的计算机的 IEEE 1394 地址空间中的地址范围和接收来自外部节点提交请求的请求\_分配\_地址\_范围请求到总线驱动程序。

当驱动程序分配的地址范围时，它可以指定哪些类型的事务的设备可能会发送到分配的地址，通过指定一个或多个访问\_标志\_类型\_读取、 访问\_标志\_类型\_写入或访问\_标志\_类型\_锁定**u.AllocateAddressRange.fulAccessType**请求的 IRB 的成员。 不指定类型之一自动的请求失败。

两个不同的驱动程序可能会分配相同的地址范围。 默认情况下，总线驱动程序自动 demultiplexes 请求，并且驱动程序只看到分配的地址来自驱动程序的设备上的请求。 驱动程序可以请求它们接收到的地址发送的总线上的所有节点，通过指定访问权限的所有数据包\_标志\_类型\_广播中的标志**u.AllocateAddressRange.fulAccessType**.

-   [分配的地址？](#ddk-receiving-asynchronous-i-o-request-packets-on-the-ieee-1394-bus-kg)
-   [分配和后备存储](#allocation-and-backing-store)
-   [有关客户端驱动程序的通知例程接收异步 I/O 请求](#client-drivers-notification-routine-for-receive-asynchronous-io-requests)
-   [在预先通知的情况下接收异步](#asynchronous-receive-in-the-pre-notification-case)

## <a name="which-addresses-are-allocated"></a>分配的地址？


总线驱动程序支持两个不同的策略分配地址范围。 如果驱动程序需要特定范围的地址，开始一个硬编码的地址，它可以指定中的硬编码地址**u.AllocateAddressRange.Required1394Offset**的请求的 IRB 和长度的成员地址范围中的**u.AllocateAddressRange.nLength**。 总线驱动程序将允许两个不同的驱动程序两次分配相同的地址。 如果相同的驱动程序会尝试分配地址范围的地址处开始相同两次，总线驱动程序将返回状态代码的状态请求\_成功，但请求本身将被忽略。

否则，该驱动程序可以允许总线驱动程序，可以选择分配的地址。 总线驱动程序跟踪所有由驱动程序，分配的地址范围，并将仅返回以前未分配的地址。

总线驱动程序不会连续分配地址。 根据作为后备存储提供 MDL 进行分段地址。 每个段中 MDL 对应于一个段中的地址范围。 需要分配的地址是连续的驱动程序可以从非分页缓冲池分配连续内存。

如果该驱动程序必须保证每个段小于特定大小，他们可以指定该大小以**u.AllocateAddressRange.MaxSegmentSize**。 驱动程序不需要指定最大段大小集**u.AllocateAddressRange.MaxSegmentSize**为零。

总线驱动程序返回中指向的内存位置的地址范围**u.AllocateAddressRange.p1394AddressRange** IRB 的成员。 设备驱动程序必须分配足够大以保存每个地址是一个数组\_范围结构，甚至在最坏的事例的细分下。 如果该驱动程序不指定段大小，或其最大段大小大于页\_大小，则该驱动程序可以通过使用地址来确定最差情形下\_AND\_大小\_TO\_跨度\_页面上的后备存储所使用的缓冲区的宏。 如果最大段大小小于页面\_大小，该驱动程序必须分配大小的数组**u.AllocateAddressRange.nLength**/**u.AllocateAddressRange.MaxSegmentSize** + 2。

当总线驱动程序返回的已分配的地址时，它记录的地址范围中分配的实际数目**u.AllocateAddressRange.hAddressRange**。

## <a name="allocation-and-backing-store"></a>分配和后备存储


总线驱动程序接收代表该驱动程序的所有异步数据包请求。 在驱动程序的是，它可以以透明方式处理该请求，或它可以将请求调度到驱动程序。 通过设置选项，当分配地址时，该驱动程序可以选择总线驱动程序如何处理每个请求。

1.  该驱动程序的地址范围，提供后备存储和总线驱动程序以透明方式处理所有的读取、 写入和锁请求使用的后备存储。

    当驱动程序分配了地址时，它可以提供在 MDL **u.AllocateAddressRange.Mdl**作为后备存储。 总线驱动程序将映射到的地址分配驱动程序和处理所有请求通过读取或写入从 MDL 范围上 MDL。 如果主机控制器支持，该事务是完全由主控制器的 DMA 硬件处理。 如果可能，请将设备驱动程序应允许总线驱动程序，若要选择的分配的地址范围： 总线驱动程序将选择的每个事务支持自动 DMA 的 1394年地址。

    该驱动程序必须指定通知\_标志\_为从不**u.AllocateAddressRange.fulNotificationOptions**。

    以下是一个示例：

    ```cpp
    pIRB->u.AllocateAddressRange.Mdl = an MDL previously allocated by the driver.
    pIRB->u.AllocateAddressRange.fulNotificationOptions = NOTIFY_FLAGS_NEVER
     
    ```

    对于此单独的选项，该驱动程序还可以分配在引发 IRQL 的地址范围。 该驱动程序可以提交直接对端口驱动程序，通过调用端口驱动程序的物理的映射例程可绕过的通信，常用的 IRP 方法的请求。 设备驱动程序将 IRB 传递给端口驱动程序的物理的映射例程。 端口驱动程序然后将分配的地址范围以异步方式;当端口驱动程序完成后，它将调用设备驱动程序的通知例程，传递**u.AllocateAddressRange.Callback**，并将传递**u.AllocateAddressRange.Context**作为参数。 在调度调用的通知例程\_级别。

    设备驱动程序可以获得一个指向端口驱动程序的物理的映射例程提交 GET\_本地\_主机\_总线驱动程序，对使用的信息请求**nLevel** = GET\_PHYS\_ADDR\_例程。 总线驱动程序返回 GET\_本地\_主机\_信息 4 结构，其中包含物理的映射例程，以及到物理的映射例程以及 IRB 将传递的设备驱动程序的上下文参数。

    下面是示例的驱动程序如何设置物理的映射例程的请求。 物理的映射例程不会更改，因此驱动程序通常仅一次提交此请求。

    ```cpp
    GET_LOCAL_HOST_INFO5 PhysMapInfo;
    pGetInfoIRB->FunctionNumber = GET_LOCAL_HOST_INFO;
    pGetInfoIRB->GET_PHYS_ADDR_ROUTINE;
     
    /* Driver submits the request. */
     
    ```

    继续上述示例，下面是该驱动程序如何使用物理的映射例程提交在提升的 irql 下完成的请求。

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

2.  驱动程序提供了后备存储的地址范围。 完成每个 I/O 事务后，总线驱动程序会通知驱动程序。

    该驱动程序可以提供单个 MDL 或 MDLs 的链接的列表作为后备存储。 如果该驱动程序提供单一 MDL，总线驱动程序将抽取数据传入或传出 MDL 以响应异步请求。 在事务完成，它通过调用驱动程序提供通知回调信号的设备驱动程序。

    设备驱动程序提供中的通知例程**u.AllocateAddressRange.Callback** IRB 的成员。 该驱动程序必须设置至少一个通知\_标志\_AFTER\_XXX 标志。 当总线驱动程序调用例程时，会传递通知\_信息结构，它指定 MDL 后备存储 (在**Mdl**)，该事务的开始位置 MDL 中的字节偏移量 (中**ulOffset**)，以及受影响的地址的范围以字节为单位的长度 (在**nLength**)。 在调度调用的通知例程\_级别。 驱动程序通过在此请求的任何上下文信息**u.AllocateAddressRange.Context**总线驱动程序中传递**上下文**通知成员\_信息。

    使用只有一个 MDL，会出现同步问题的风险： 设备可能快于驱动程序可从其中读取写入的地址范围。 若要避免此类冲突，向其设备仅具有写访问权限，驱动程序的地址可以在提供 MDLs 的链接的列表**u.AllocateAddressRange.FifoSListHead**，并进行锁定数值调节钮**u。AllocateAddressRange.FifoSpinLock**。 当总线驱动程序收到每个异步请求数据包时，它持有自旋锁，并弹出关闭列表来完成该请求上的第一个元素。 然后，它调用驱动程序的通知例程。

    在通知\_信息结构总线驱动程序提供了使用它来处理事务 MDL (在**Mdl**)，受影响的第一个地址的字节偏移量 (在**ulOffset**)，并受影响的地址的范围的长度 (在**nLength**)。 它还提供了地址\_MDL 的先进先出 (在**Fifo**)。 驱动程序从其通知例程将返回之前，它应使用**Fifo**将元素推送回在列表中，或提供的相同的另一个 MDL 大小; 否则为总线驱动程序将耗尽 MDLs 用于处理写入从设备请求。

    下面是通知的使用此类型的扩展的示例。 全局范围内，驱动程序创建一个互锁、 单向链接列表中和自旋锁。 该驱动程序需要访问链接的列表和在引发于 Irql，旋转锁，因此它们必须在非分页内存中。 通常情况下，驱动程序将它们保留在其设备扩展。

    ```cpp
    PSLIST_HEADER FifoSListHead;
    KSPIN_LOCK FifoSpinLock;
     
    ExInitializeSListHead(FifoSListHead);
    KeInitializeSpinLock(FifoSpinLock);
     
    ```

    该驱动程序提交请求时，它可以按如下所示设置相关的 IRB 成员：

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

    在回调中，该驱动程序是需要分配新 MDL 并将其推送到列表中，或推送原始 MDL 重新打开列表。 对于后者，总线驱动程序将传递的原始地址\_先进先出的当前 MDL。 下面是将当前 MDL 推送回列表上的驱动程序示例：

    ```cpp
    ExInterlockedPushEntrySList(FifoSListHead, NotificationInfo->Fifo->FifoList, FifoSpinLock);
     
    ```

    如果该驱动程序指定单一 MDL 作为后备存储在原始的分配请求，则驱动程序可能会返回一个或多个地址范围。

3.  每次请求到达时，并关闭驱动程序的数据包，总线驱动程序发出信号，驱动程序。

    该驱动程序提供了在回调**u.AllocateAddressRange.Callback** IRB 的成员。 NOTIFY\_标志\_AFTER\_XXX 标志将被忽略，并且所有数据包都传递给驱动程序来处理。

    该驱动程序必须设置**Mdl**， **FifoSListHead**，并**FifoSpinLock**的成员**u.AllocateAddressRange**到**NULL**。 下面是想要接收的所有三种类型的异步请求数据包时收到通知的驱动程序的设置的示例。

    ```cpp
    VOID DriverNotificationRoutine( IN PNOTIFICATION_INFO NotificationInfo );
     
    pIRB->u.AllocateAddressRange.Callback = DriverNotificationRoutine;
    pIRB->u.AllocateAddressRange.Context = information specific to this address range.
    pIRB->u.AllocateAddressRange.Mdl = NULL;
    pIRB->u.AllocateAddressRange.FifoSListHead = NULL;
    pIRB->u.AllocateAddressRange.FifoSpinLock = NULL;
     
    ```

    总线驱动程序会分配单个连续范围的地址。

    总线驱动程序将通知传递\_信息结构与驱动程序的回调例程。 设备驱动程序必须创建其自己的响应数据包 （请参阅详细信息的 IEEE 1394 规范），并且它必须分配其自己的缓冲区来包含它创建的响应数据包。 响应数据包必须从非分页池或已探测并锁定的缓冲区中。

    在通知内\_信息，总线驱动程序提供了在未初始化的 MDL **ResponseMdl**成员。 它还提供了指向其中它期望输入一个指针，以响应数据包的设备驱动程序的内存位置的指针 (在**ResponsePacket**)，和响应数据包长度 (在**ResponseLength**)。 该驱动程序还可以提供一个内核事件对象。 完成事务后，总线驱动程序发出信号内核事件对象。

    下面是举例说明如何将设备驱动程序可以填写其通知例程中所需的信息。

    ```cpp
    /* Suppose the driver creates its response packet in PVOID ResponsePacket, of length ResponseLength. It has created a kernel event ResponseEvent. */
    MmInitializeMdl(NotificationInfo->ResponseMdl, ResponsePacket, ResponseLength);
    MmBuildMdlFForNonPagedPool(Notification->ResponseMdl);
    *(NotificationInfo->ResponsePacket) = ResponsePacket.
    *(NotificationInfo->ResponseLength) = ResponseLength;
    *(NotificationInfo)->ResponseEvent = Event;
     
    ```

## <a name="client-drivers-notification-routine-for-receive-asynchronous-io-requests"></a>有关客户端驱动程序的通知例程接收异步 I/O 请求


客户端驱动程序必须执行以下任务中的驱动程序的异步接收通知例程：

-   验证的成员[**通知\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff537437)传递给客户端驱动程序的结构。
-   对于成功的读锁请求 （其中返回的响应数据包通过数据），客户端驱动程序必须：
    -   通过调用分配的内存[ **WdfMemoryCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff548706) ([**ExAllocatePoolWithTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544520) WDM 基于客户端驱动程序) 的响应数据包数据。
    -   与要返回的数据填充该缓冲区。
    -   初始化**ResponseMdl**成员和引用缓冲区。 您可以调用[ **MmInitializeMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff554568)并[ **MmBuildMdlForNonPagedPool**](https://msdn.microsoft.com/library/windows/hardware/ff554498)。
    -   设置 **\*NotificationInfo-&gt;ResponsePacket**以指向缓冲区。
    -   设置 **\*NotificationInfo-&gt;ResponseLength**到返回的响应数据的大小，这是 4 quadlet 读取请求)。
    -   通过调用分配的内存[ **WdfMemoryCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff548706) ([**ExAllocatePoolWithTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544520) WDM 基于客户端驱动程序) 的响应事件。
    -   设置 **\*NotificationInfo-&gt;ResponseEvent**以指向事件缓冲区。
    -   计划要等待该事件的工作项和响应事件收到信号后释放响应数据包和事件数据缓冲区。
    -   设置**NotificationInfo-&gt;ResponseCode**到 RCODE\_响应\_完成。

## <a name="asynchronous-receive-in-the-pre-notification-case"></a>在预先通知的情况下接收异步


旧的 1394年总线驱动程序无法正常工作，以完成异步接收事务使用的预先通知机制。 有关详细信息，请参阅[知识库：IEEE 1394 异步接收响应不使用预通知 (2635883) 发送](http://support.microsoft.com/kb/2635883)。

对于新的 1394年总线驱动程序，在预先通知的情况下，客户端驱动程序的通知回调例程的预期的行为如下所示：

-   如果**Mdl**并**Fifo**的成员[**通知\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff537437)结构均为 NULL，然后预通知正在执行。
-   **ResponseMdl**， **ResponsePacket**， **ResponseLength**，以及**ResponseEvent**成员[ **通知\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff537437)结构不能为 NULL。
-   **FulNotificationOptions**的成员[**通知\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff537437)结构必须指示触发的操作 （读取、 写入、 锁定）通知。 只有一个标志 (NOTIFY\_标志\_AFTER\_读取、 通知\_标志\_AFTER\_写入或通知\_标志\_AFTER\_锁) 可以设置每次调用通知例程时。
-   你可以通过检查确定请求的类型**RequestPacket-&gt;AP\_tCode**异步成员\_数据包结构。 该成员指示 TCODE，指定的请求类型，如阻止或 quadlet 读/写，锁请求的类型。 ASYNC\_中 1394.h 声明数据包结构。
-   **ResponsePacket**并**ResponseEvent**的成员[**通知\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff537437)包含指向指针的指针。 因此，必须适当地引用指向您的响应数据包和响应事件。
-   **ResponseLength**的成员[**通知\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff537437)指向 ULONG 变量的指针。 因此，您必须设置请求的响应数据长度与读取此类时相应地取消引用成员与锁定请求）。
-   1394 客户端驱动程序负责分配的内存的响应数据包和响应事件 （从非分页缓冲池），并传递响应之后释放该内存。 建议的工作项排入队列和工作项应等待响应事件。 该事件发出信号后响应已发送的 1394年总线驱动程序。 客户端驱动程序然后可以释放的内存中工作项。
-   **ResponseCode**中的成员[**通知\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff537437)结构必须设置为 1394.h 中定义的 RCODE 值之一。 如果**ResponseCode**设置为 RCODE 以外的任何值\_响应\_完成，1394年总线驱动程序将发送错误响应数据包。 如果读取或锁请求，请求未返回任何数据。 在 Windows 7 中，可能会泄漏内存的详细信息，请参阅[知识库：IEEE 1394 总线驱动程序执行异步通知回调 (2023232) 中的内存泄漏](http://support.microsoft.com/kb/2023232)。
-   对于读取和锁的请求， **ResponsePacket**的成员[**通知\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff537437)结构必须指向要在中返回的数据异步响应数据包。

下面的代码示例显示了工作项实施方案和客户端驱动程序的通知例程。

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

 

 




