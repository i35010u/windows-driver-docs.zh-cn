---
title: 支持被动级别中断
description: 从框架 1.11 版开始，WDF 驱动程序可以创建需要被动级别处理的中断对象。
ms.assetid: E464F885-928C-40BC-A09F-7A7921F8FF37
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e08dfa1d9ae8348241e043af442b6407502c20f6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368060"
---
# <a name="supporting-passive-level-interrupts"></a>支持被动级别中断


从框架版本 1.11，内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF) 开始 Windows 8 或更高版本的操作系统上运行的驱动程序可以创建需要被动级别处理的中断对象。 如果驱动程序配置被动级别中断处理的中断对象，框架将调用驱动程序的中断服务例程 (ISR) 和其他[中断对象事件的回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/)在 IRQL = 被动\_同时保留被动级别中断锁定级别。

如果要针对系统芯片 (SoC) 平台上开发基于 framework 的驱动程序，可以使用被动模式下中断通过低速总线，如 I²C、 SPI 或 UART 与关闭 SoC 设备进行通信。

否则，应使用[需要在设备的 IRQL 处进行处理的中断](creating-an-interrupt-object.md)(DIRQL)。 如果您的驱动程序支持消息信号中断 (Msi)，则必须使用 DIRQL 中断处理。 在版本 1.9 及更早版本中，框架会始终处理中断在 IRQL = DIRQL。

本主题介绍如何[创建](#creating-a-passive-level-interrupt)，[服务](#servicing)，并[同步](#synchronizing)被动等级中断。

## <a name="creating-a-passive-level-interrupt"></a>创建一个被动级别中断


若要创建一个被动级别中断对象，驱动程序必须初始化[ **WDF\_中断\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)结构并将其传递给[ **WdfInterruptCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)方法。 配置结构，该驱动程序应：

-   设置**PassiveHandling**成员为 TRUE。
-   提供[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调函数，以在被动级别调用。
-   （可选） 设置**AutomaticSerialization**为 TRUE。 如果驱动程序设置**AutomaticSerialization**为 TRUE，则框架将同步执行的中断对象[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)或[*EvtInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)从中断的父对象下的其他对象的回调函数的回调函数。
-   （可选） 该驱动程序都可以提供[ *EvtInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)回调函数调用在 IRQL = 被动\_级别，或[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数调用在 IRQL = 调度\_级别。

设置上述配置结构的成员的其他信息，请参阅[ **WDF\_中断\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)。
有关启用和禁用被动等级中断的信息，请参阅[启用和禁用中断](enabling-and-disabling-interrupts.md)。

## <a href="" id="servicing"></a>服务的被动级别中断


[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调函数，运行在 IRQL = 被动\_中断与所持有的被动级别中断锁级别，通常按计划工作项或中断到 DPC处理在更高版本时与中断相关的信息。 基于框架的驱动程序实现工作项或作为 DPC 例程[ *EvtInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)或[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数。

若要计划的执行[ *EvtInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)回调函数，驱动程序调用[ **WdfInterruptQueueWorkItemForIsr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueueworkitemforisr)内[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调函数。

若要计划的执行[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数，驱动程序调用[ **WdfInterruptQueueDpcForIsr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueuedpcforisr)从内[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调函数。 (回想一下，驱动程序的*EvtInterruptIsr*回调函数可以调用[ **WdfInterruptQueueWorkItemForIsr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueueworkitemforisr)或**WdfInterruptQueueDpcForIsr**，但不可同时使用两者。)

大多数驱动程序使用单个[ *EvtInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)或[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)中断每种类型的回调函数。 如果您的驱动程序创建多个框架为每个设备的中断对象，请考虑使用单独*EvtInterruptWorkItem*或*EvtInterruptDpc*每个中断的回调。

驱动程序通常完成 I/O 请求在其[ *EvtInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)或[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数。

下面的代码示例演示如何使用被动等级中断的驱动程序可能会安排[ *EvtInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)回调中的其[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)函数。

```cpp
BOOLEAN

EvtInterruptIsr(
    _In_  WDFINTERRUPT Interrupt,
    _In_  ULONG        MessageID
    )
/*++

  Routine Description:

    This routine responds to interrupts generated by the hardware.
    It stops the interrupt and schedules a work item for 
    additional processing.

    This ISR is called at PASSIVE_LEVEL (passive-level interrupt handling).

  Arguments:
  
    Interrupt - a handle to a framework interrupt object
    MessageID - message number identifying the device's
        hardware interrupt message (if using MSI)

  Return Value:

    TRUE if interrupt recognized.

--*/
{
    
    UNREFERENCED_PARAMETER(MessageID);

    NTSTATUS                status;
    PDEV_CONTEXT            devCtx;
    WDFREQUEST              request;
    WDF_MEMORY_DESCRIPTOR   memoryDescriptor;
    INT_REPORT              intReport = {0};
    BOOLEAN                 intRecognized;
    WDFIOTARGET             ioTarget;
    ULONG_PTR               bytes;
    WDFMEMORY               reqMemory;

    intRecognized = FALSE;

    //         
    // Typically the pattern in most ISRs (DIRQL or otherwise) is to:
    // a) Check if the interrupt belongs to this device (shared interrupts).
    // b) Stop the interrupt if the interrupt belongs to this device.
    // c) Acknowledge the interrupt if the interrupt belongs to this device.
    //
   
   
    //
    // Retrieve device context so that we can access our queues later.
    //    
    devCtx = GetDevContext(WdfInterruptGetDevice(Interrupt));

     
    //
    // Init memory descriptor.
    //    
    WDF_MEMORY_DESCRIPTOR_INIT_BUFFER(
                         &memoryDescriptor,
                         &intReport,
                         sizeof(intReport);

    //
    // Send read registers/data IOCTL. 
    // This call stops the interrupt and reads the data at the same time.
    // The device will reinterrupt when a new read is sent.
    //
    bytes = 0;
    status = WdfIoTargetSendIoctlSynchronously(
                             ioTarget,
                             NULL,
                             IOCTL_READ_REPORT,
                             &memoryDescriptor,
                             NULL,
                             NULL,
                             &bytes);
     
    //
    // Return from ISR if this is not our interrupt.
    // 
    if (intReport->Interrupt == FALSE) {
        goto exit;
    }

    intRecognized = TRUE;

    //
    // Validate the data received.
    //
    ...

    //
    // Retrieve the next read request from the ReportQueue which
    // stores all the incoming IOCTL_READ_REPORT requests
    // 
    request = NULL;
    status = WdfIoQueueRetrieveNextRequest(
                            devCtx->ReportQueue,
                            &request);

    if (!NT_SUCCESS(status) || (request == NULL)) {
        //
        // No requests to process. 
        //
        goto exit;
    }
    
    //
    // Retrieve the request buffer.
    //
    status = WdfRequestRetrieveOutputMemory(request, &reqMemory);

    //
    // Copy the data read into the request buffer.
    // The request will be completed in the work item.
    //
    bytes = intReport->Data->Length;
    status = WdfMemoryCopyFromBuffer(
                            reqMemory,
                            0,
                            intReport->Data,
                            bytes);

    //
    // Report how many bytes were copied.
    //
    WdfRequestSetInformation(request, bytes);

    //
    // Forward the request to the completion queue.
    //
    status = WdfRequestForwardToIoQueue(request, devCtx->CompletionQueue);
    
    //
    // Queue a work-item to complete the request.
    //
    WdfInterruptQueueWorkItemForIsr(FxInterrupt);

exit:
    return intRecognized;
}

VOID
EvtInterruptWorkItem(
    _In_ WDFINTERRUPT   Interrupt,
    _In_ WDFOBJECT      Device
    )
/*++

Routine Description:

    This work item handler is triggered by the interrupt ISR.

Arguments:

    WorkItem - framework work item object

Return Value:

    None

--*/
{
    UNREFERENCED_PARAMETER(Device);

    WDFREQUEST              request;
    NTSTATUS                status;
    PDEV_CONTEXT            devCtx;
    BOOLEAN                 run, rerun;
    
    devCtx = GetDevContext(WdfInterruptGetDevice(Interrupt));

    WdfSpinLockAcquire(devCtx->WorkItemSpinLock);
    if (devCtx->WorkItemInProgress) {
        devCtx->WorkItemRerun = TRUE;
        run = FALSE;
    }
    else {
        devCtx->WorkItemInProgress = TRUE;
        devCtx->WorkItemRerun = FALSE;
        run = TRUE;
    }
    WdfSpinLockRelease(devCtx->WorkItemSpinLock);

    if (run == FALSE) {
        return;
    }

    do {  
        for (;;) {
            //
            // Complete all report requests in the completion queue.
            //
            request = NULL;
            status = WdfIoQueueRetrieveNextRequest(devCtx->CompletionQueue, 
                                                   &request);
            if (!NT_SUCCESS(status) || (request == NULL)) {
                break;
            }
            
            WdfRequestComplete(request, STATUS_SUCCESS);
        }
        
        WdfSpinLockAcquire(devCtx->WorkItemSpinLock);
        if (devCtx->WorkItemRerun) {
            rerun = TRUE;
            devCtx->WorkItemRerun = FALSE;
        }
        else {
            devCtx->WorkItemInProgress = FALSE;
            rerun = FALSE;
        }
        WdfSpinLockRelease(devCtx->WorkItemSpinLock);
    }
    while (rerun);
}

VOID
EvtIoInternalDeviceControl(
    _In_  WDFQUEUE      Queue,
    _In_  WDFREQUEST    Request,
    _In_  size_t        OutputBufferLength,
    _In_  size_t        InputBufferLength,
    _In_  ULONG         IoControlCode
    )
{
    NTSTATUS            status;
    DEVICE_CONTEXT      devCtx;
    devCtx = GetDeviceContext(WdfIoQueueGetDevice(Queue));
    
    switch (IoControlCode) 
    {
    ...
    case IOCTL_READ_REPORT:

        //
        // Forward the request to the manual ReportQueue to be completed
        // later by the interrupt work item.
        //
        status = WdfRequestForwardToIoQueue(Request, devCtx->ReportQueue);
        break;
   
    ...
    }

    if (!NT_SUCCESS(status)) {
        WdfRequestComplete(Request, status);
    }
}
```

## <a href="" id="synchronizing"></a>同步被动级别中断


若要防止死锁，请编写一个实现被动级别中断处理的驱动程序时遵循以下准则：

-   如果**AutomaticSerialization**设置为 TRUE，应执行的操作未[发送同步请求](sending-i-o-requests-synchronously.md)中[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)或[ *EvtInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)回调函数。
-   释放之前被动级别中断锁[完成 I/O 请求](completing-i-o-requests.md)。
-   提供[ *EvtInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)， [ *EvtInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)，并[ *EvtInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)根据需要。
-   如果您的驱动程序必须与中断相关的工作，在任意线程上下文中，如执行中[请求处理程序](request-handlers.md)，使用[ **WdfInterruptTryToAcquireLock** ](https://msdn.microsoft.com/library/windows/hardware/hh439284)并[**WdfInterruptReleaseLock**](https://msdn.microsoft.com/library/windows/hardware/ff547376)。 不要调用[ **WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340)， [ **WdfInterruptSynchronize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptsynchronize)， [ **WdfInterruptEnable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptenable)，或[ **WdfInterruptDisable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptdisable)从任意线程上下文。 有关可以通过调用导致死锁方案的示例**WdfInterruptAcquireLock**从任意线程上下文，请参阅备注部分[ **WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340).

    如果在调用[ **WdfInterruptTryToAcquireLock** ](https://msdn.microsoft.com/library/windows/hardware/hh439284)失败，该驱动程序将推迟到工作项及其与中断相关的工作。 在该工作项，该驱动程序可以安全地获取中断锁通过调用[ **WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340)。 有关详细信息，请参阅[ **WdfInterruptTryToAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/hh439284)。

    该驱动程序可以调用在非任意线程上下文中，工作项，如[ **WdfInterruptAcquireLock** ](https://msdn.microsoft.com/library/windows/hardware/ff547340)或[ **WdfInterruptSynchronize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptsynchronize).

有关使用中断锁的详细信息，请参阅[同步中断代码](synchronizing-interrupt-code.md)。

 

 





