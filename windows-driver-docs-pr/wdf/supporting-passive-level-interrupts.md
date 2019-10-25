---
title: 支持被动级别中断
description: 从 framework 版本1.11 开始，WDF 驱动程序可以创建需要被动级别处理的中断对象。
ms.assetid: E464F885-928C-40BC-A09F-7A7921F8FF37
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24d99eadcc8999e3dd2daec4e7639f3a67f221c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831728"
---
# <a name="supporting-passive-level-interrupts"></a>支持被动级别中断


从 framework 版本1.11 开始，在 Windows 8 或更高版本的操作系统上运行的内核模式驱动程序框架（KMDF）和用户模式驱动程序框架（UMDF）驱动程序可以创建需要被动级别处理的中断对象。 如果驱动程序为被动级别中断处理配置了中断对象，则框架将调用驱动程序的中断服务例程（ISR）和其他[中断对象事件回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/)，同时\_在被动级别中断锁。

如果要为芯片（SoC）平台上的系统开发基于框架的驱动程序，可以使用被动模式中断，通过低速总线（例如，I-C、SPI 或 UART）与离 SoC 设备进行通信。

否则，应使用[需要在设备的 IRQL （DIRQL）上处理的中断](creating-an-interrupt-object.md)。 如果驱动程序支持消息终止中断（Msi），则必须使用 DIRQL 中断处理。 在版本1.9 及更早版本中，框架始终以 IRQL = DIRQL 处理中断。

本主题介绍如何[创建](#creating-a-passive-level-interrupt)、[服务](#servicing)和[同步](#synchronizing)被动级中断。

## <a name="creating-a-passive-level-interrupt"></a>创建被动级中断


若要创建被动级别中断对象，驱动程序必须初始化[**WDF\_中断\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)结构并将其传递给[**WdfInterruptCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)方法。 在配置结构中，驱动程序应：

-   将**PassiveHandling**成员设置为 TRUE。
-   提供要在被动级别调用的[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调函数。
-   可以选择将**AutomaticSerialization**设置为 TRUE。 如果驱动程序将**AutomaticSerialization**设置为 TRUE，则框架会将中断对象的[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)或[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)回调函数的执行与其他对象中的回调函数同步，位于中断的父对象下。
-   或者，驱动程序可以提供一个[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)回调函数，以 IRQL = 被动\_级别或[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数调用，以 IRQL = 调度\_级别调用。

有关设置上述配置结构成员的其他信息，请参阅[**WDF\_中断\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)。
有关启用和禁用被动级中断的信息，请参阅[启用和禁用中断](enabling-and-disabling-interrupts.md)。

## <a href="" id="servicing"></a>为被动级别中断提供服务


[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调函数在具有被动级别中断锁的情况下运行时，该函数以 IRQL = 被动\_级别运行，通常计划中断工作项或中断 DPC 稍后处理与中断相关的信息。 基于框架的驱动程序将工作项或 DPC 例程作为[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)或[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数来实现。

若要计划[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)回调函数的执行，驱动程序从[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调函数中调用[**WdfInterruptQueueWorkItemForIsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueueworkitemforisr) 。

若要计划[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数的执行，驱动程序从[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调函数中调用[**WdfInterruptQueueDpcForIsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueuedpcforisr) 。 （回想一下，驱动程序的*EvtInterruptIsr*回调函数可以调用[**WdfInterruptQueueWorkItemForIsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueueworkitemforisr)或**WdfInterruptQueueDpcForIsr**，但不能同时调用两者。）

大多数驱动程序对每种类型的中断使用单个[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)或[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数。 如果驱动程序为每个设备创建了多个框架中断对象，请考虑对每个中断使用单独的*EvtInterruptWorkItem*或*EvtInterruptDpc*回调。

驱动程序通常会在其[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)或[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数中完成 i/o 请求。

下面的代码示例演示如何使用被动级别中断的驱动程序在其[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)函数内计划[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)回调。

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


若要防止死锁，请在编写实现被动级中断处理的驱动程序时遵循以下准则：

-   如果**AutomaticSerialization**设置为 TRUE，则不要从[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)或[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)回调函数中[发送同步请求](sending-i-o-requests-synchronously.md)。
-   在[完成 i/o 请求](completing-i-o-requests.md)之前释放被动级中断锁。
-   必要时提供[*EvtInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)、 [*EvtInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)和[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem) 。
-   如果驱动程序必须在任意线程上下文中执行与中断相关的工作，例如在[请求处理程序](request-handlers.md)中，请使用[**WdfInterruptTryToAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/hh439284)和[**WdfInterruptReleaseLock**](https://msdn.microsoft.com/library/windows/hardware/ff547376)。 不要从任意线程上下文调用[**WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340)、 [**WdfInterruptSynchronize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptsynchronize)、 [**WdfInterruptEnable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptenable)或[**WdfInterruptDisable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptdisable) 。 有关可以通过从任意线程上下文调用**WdfInterruptAcquireLock**而导致的死锁情况示例，请参阅[**WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340)的 "备注" 部分。

    如果对[**WdfInterruptTryToAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/hh439284)的调用失败，则驱动程序可以将与中断相关的工作推迟到工作项。 在该工作项中，驱动程序可以通过调用[**WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340)来安全地获取中断锁。 有关详细信息，请参阅[**WdfInterruptTryToAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/hh439284)。

    在非任意线程上下文（如工作项）中，驱动程序可以调用[**WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340)或[**WdfInterruptSynchronize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptsynchronize)。

有关使用中断锁的详细信息，请参阅[同步中断代码](synchronizing-interrupt-code.md)。

 

 





