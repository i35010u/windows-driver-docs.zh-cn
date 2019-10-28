---
title: 存储筛选器驱动程序的调度例程
description: 存储筛选器驱动程序的调度例程
ms.assetid: 0d1af035-537f-4632-800b-eb344dc5a3c8
keywords:
- 存储筛选器驱动程序 WDK，调度例程
- 筛选器驱动程序 WDK 存储，调度例程
- SFD WDK 存储，调度例程
- 调度例程 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8da312423c442c25282d022da3fbc61c6594a38f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844480"
---
# <a name="storage-filter-drivers-dispatch-routines"></a>存储筛选器驱动程序的调度例程


## <span id="ddk_storage_filter_drivers_dispatch_routines_kg"></span><span id="DDK_STORAGE_FILTER_DRIVERS_DISPATCH_ROUTINES_KG"></span>


与任何其他更高级的内核模式驱动程序一样，存储筛选器驱动程序（SFD）必须具有一个或多个*调度*例程来处理每个 IRP\_MJ\_XXX 请求，基础存储驱动程序为这些请求提供*调度*入口点. 根据其设备的性质，SFD 的*调度*入口点可能会对任何给定的请求执行以下操作之一：

-   对于不需要特殊处理的请求，请在 IRP 中为下一个较低版本的驱动程序设置 i/o 堆栈位置，可能调用[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)为 irp 设置其[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，并通过降低驱动程序的[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)。

-   对于已由存储类驱动程序处理的请求，在设置 i/o 堆栈位置之前修改 IRP 的 i/o 堆栈位置中的 SRB，可能需要设置[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，并将 IRP 传递到带有[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)的下一个低版本驱动程序。

-   使用 SRB 和 CDB 为其设备设置新的 IRP，调用[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) ，以便 SRB （和 irp （如果驱动程序调用[**IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)或[**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)）可以释放，并通过[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)传递 irp

    SFD 最有可能使用主功能代码[**IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)设置新的 irp。

## <a name="span-idprocessing_requestsspanspan-idprocessing_requestsspanspan-idprocessing_requestsspanprocessing-requests"></a><span id="Processing_requests"></span><span id="processing_requests"></span><span id="PROCESSING_REQUESTS"></span>处理请求


对于不需要特殊处理的请求，SFD 的*调度*例程通常使用输入 IRP 调用[**IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) ，然后使用指向类驱动程序的设备对象和 IRP 的指针调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 。 请注意，SFD 很少在 Irp 中设置不需要特殊处理的[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，因为对*IoCompletion*例程的调用是不必要的，因为它会降低驱动程序设备的 i/o 吞吐量。 如果 SFD 设置了*IoCompletion*例程，它将调用[**IoCopyCurrentIrpStackLocationToNext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)而不是**IoSkipCurrentIrpStackLocation** ，然后在调用**IoSetCompletionRoutine**之前调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine) 。

对于需要特殊处理的请求，SFD 可以执行以下操作：

1.  创建具有[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)、 [**IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)、 [**IOBUILDSYNCHRONOUSFSDREQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)或[**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)的新 IRP，通常为自身指定 i/o 堆栈位置。

2.  如果无法分配 IRP，请检查返回的 IRP 指针是否有**NULL**和返回**状态\_资源不足\_资源**。

3.  如果驱动程序创建的 IRP 包含 SFD 的 i/o 堆栈位置，请调用[**IoSetNextIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetnextirpstacklocation)来设置 IRP 堆栈位置指针。 然后，调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)以获取指向驱动程序创建的 IRP 中其自己的 i/o 堆栈位置的指针，并将其设置为由其自己的[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程使用的状态。

4.  调用[**IoGetNextIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)可获取指向驱动程序创建的 IRP 中下一个较低驱动程序的 i/o 堆栈位置的指针，并将其设置为主要功能代码**IRP\_MJ\_SCSI**和 SRB （请参阅[存储类驱动程序](storage-class-drivers.md)）。

5.  如有必要，将要传输到设备的数据转换为特定于设备的非标准格式。

6.  如果驱动程序为 SRB、SCSI 请求感知缓冲区、MDL 和/或 IRP 调用了[**IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)或[**IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)的内存，或者如果驱动程序必须转换，请调用[**IoSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutine)从设备以设备特定的非标准格式传输的数据。

7.  使用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)将驱动程序创建的 IRP 传递到下一个较低的驱动程序。

## <a name="span-idhandling_srb_formatsspanspan-idhandling_srb_formatsspanspan-idhandling_srb_formatsspanhandling-srb-formats"></a><span id="Handling_SRB_formats"></span><span id="handling_srb_formats"></span><span id="HANDLING_SRB_FORMATS"></span>处理 SRB 格式


从 Windows 8 开始，类驱动程序和端口驱动程序之间的 SFD 筛选必须检查是否支持 SRB 格式。 具体而言，这涉及到检测 SRB 格式并正确地访问结构的成员。 IRP 中的 SRB 为[**SCSI\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)和或[**存储\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_storage_request_block)。 筛选器驱动程序可以提前确定下面的端口驱动程序所支持的 SRBs，方法是[ **\_属性请求发出 IOCTL\_存储\_查询**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)，并指定**StorageAdapterProperty**标识符。 [**存储\_适配器\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor)结构中返回的**SrbType**和**AddressType**值指示端口驱动程序使用的 SRB 格式和寻址方案。 筛选器驱动程序分配和发送的任何新 SRBs 必须是该查询所返回的类型。

同样，从 Windows 8 开始，仅支持[**SCSI\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)类型的 SRBs 的 SFDs 必须检查[**存储\_适配器\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_adapter_descriptor)结构中返回的**SrbType**值是否设置为**SRB\_类型\_SCSI\_请求\_块**。 若要处理将**SrbType**设置为**SRB\_键入\_存储\_请求\_块**的情况，筛选器驱动程序必须为[**IOCTL\_存储\_查询设置完成例程\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_query_property)当**StorageAdapterProperty**标识符在其上方的驱动程序发送的请求中设置时，为属性。 完成例程会将**存储\_适配器\_描述符**中的**SrbType**成员修改为**SRB\_类型\_SCSI\_请求\_块**以正确设置支持的类型。

下面是一个用于处理这两种 SRB 格式的筛选器调度例程的示例。

```ManagedCPlusPlus
NTSTATUS FilterScsiIrp(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp
    )
{
    PFILTER_DEVICE_EXTENSION  deviceExtension = DeviceObject->DeviceExtension;
    PIO_STACK_LOCATION irpStack = IoGetCurrentIrpStackLocation(Irp);
    NTSTATUS status;
    PSCSI_REQUEST_BLOCK srb;   
    ULONG srbFunction;
    ULONG srbFlags;

    //
    // Acquire the remove lock so that device will not be removed while
    // processing this irp.
    //

    status = IoAcquireRemoveLock(&deviceExtension->RemoveLock, Irp);

    if (!NT_SUCCESS(status)) {
        Irp->IoStatus.Status = status;
        IoCompleteRequest(Irp, IO_NO_INCREMENT);
        return status;
    }

    srb = irpStack->Parameters.Scsi.Srb;
     
    if (srb->Function == SRB_FUNCTION_STORAGE_REQUEST_BLOCK) {
        srbFunction = ((PSTORAGE_REQUEST_BLOCK)srb)->SrbFunction;
        srbFlags = ((PSTORAGE_REQUEST_BLOCK)srb)->SrbFlags;
    } else {
        srbFunction = srb->Function;
        srbFlags = srb->SrbFlags;
    }

    if (srbFunction == SRB_FUNCTION_EXECUTE_SCSI) {
        if (srbFlags & SRB_FLAGS_UNSPECIFIED_DIRECTION) {
            // ...

            // filter processing for SRB_FUNCTION_EXECUTE_SCSI

            // ...
        }
    }

    IoMarkIrpPending(Irp);
    IoCopyCurrentIrpStackLocationToNext(Irp);
    IoSetCompletionRoutine(Irp,
                           FilterScsiIrpCompletion,
                           DeviceExtension->DeviceObject,
                           TRUE, TRUE, TRUE);
    IoCallDriver(DeviceExtension->TargetDeviceObject, Irp);

    return STATUS_PENDING; 
}
```

## <a name="span-idsetting_up_requestsspanspan-idsetting_up_requestsspanspan-idsetting_up_requestsspansetting-up-requests"></a><span id="Setting_up_requests"></span><span id="setting_up_requests"></span><span id="SETTING_UP_REQUESTS"></span>设置请求


与存储类驱动程序一样，SFD 可能具有要从驱动程序的*调度*例程调用的*BuildRequest*或*SplitTransferRequest*例程，或者可能会实现内联相同的功能。

有关*BuildRequest*和*SplitTransferRequest*例程的详细信息，请参阅[存储类驱动程序](storage-class-drivers.md)。 有关*调度*例程一般要求的详细信息，请参阅[编写调度例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-dispatch-routines)。

 

 




