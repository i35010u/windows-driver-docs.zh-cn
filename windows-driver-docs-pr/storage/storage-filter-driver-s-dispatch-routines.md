---
title: 存储筛选器驱动程序的调度例程
description: 存储筛选器驱动程序的调度例程
ms.assetid: 0d1af035-537f-4632-800b-eb344dc5a3c8
keywords:
- 存储筛选器驱动程序 WDK、 调度例程
- 筛选器驱动程序 WDK 存储中，调度例程
- SFD WDK 存储，调度例程
- 调度例程 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e78855318fcb20d5d6a25166cd49712c03d8b83b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370431"
---
# <a name="storage-filter-drivers-dispatch-routines"></a>存储筛选器驱动程序的调度例程


## <span id="ddk_storage_filter_drivers_dispatch_routines_kg"></span><span id="DDK_STORAGE_FILTER_DRIVERS_DISPATCH_ROUTINES_KG"></span>


像任何其他更高级别的内核模式驱动程序，存储筛选器驱动程序 (SFD) 必须具有一个或多个*调度*例程来处理每个 IRP\_MJ\_XXX 请求为其基础存储驱动程序提供*调度*入口点。 具体取决于其设备的性质*调度*SFD 入口点可能会执行任何给定请求的以下值之一：

-   需要设置中的下一步较低的驱动程序，IRP 的 I/O 堆栈位置没有特殊处理的请求可能是调用[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)若要设置其[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程的 IRP，并传递进行进一步处理低级驱动程序与上 IRP [ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)。

-   对于已由存储类驱动程序处理请求，修改 SRB IRP 的 I/O 堆栈位置中设置的 I/O 堆栈位置之前，可能是将[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程，并传递 IRP与下一步低驱动程序带有[ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)。

-   设置新 IRP SRB 和 CDB 对于其设备，请调用[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)因此 SRB (和 IRP 如果驱动程序调用[ **IoAllocateIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)或[ **IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildasynchronousfsdrequest)) 可释放，并将 IRP 传递[ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)

    SFD 是最有可能设置了主要函数代码与新 Irp [ **IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)。

## <a name="span-idprocessingrequestsspanspan-idprocessingrequestsspanspan-idprocessingrequestsspanprocessing-requests"></a><span id="Processing_requests"></span><span id="processing_requests"></span><span id="PROCESSING_REQUESTS"></span>处理请求


对于不需要任何特殊的处理的请求*调度*SFD 例程通常调用[ **IoSkipCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)与输入的 IRP，然后调用[**IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)与类驱动程序的设备对象和 IRP 的指针。 请注意，SFD 很少设置其[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程不需要任何特殊处理这两个，因为 Irp 中调用*IoCompletion*例程是不必要和因为它会降低，驱动程序的设备的 I/O 吞吐量。 如果未设置 SFD *IoCompletion*例程，它将调用[ **IoCopyCurrentIrpStackLocationToNext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocopycurrentirpstacklocationtonext)而不是**IoSkipCurrentIrpStackLocation** ，然后调用[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)之前，调用**IoCallDriver**。

对于需要特殊处理的请求，SFD 可以执行以下操作：

1.  创建与新 IRP [ **IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)， [ **IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)， [ **IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildsynchronousfsdrequest)，或[ **IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildasynchronousfsdrequest)，通常为本身指定的 I/O 堆栈位置。

2.  检查为返回的 IRP 指针**NULL** ，并返回**状态\_不足\_资源**如果无法分配 IRP。

3.  如果驱动程序创建 IRP 为 SFD 包括 I/O 堆栈位置，调用[ **IoSetNextIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetnextirpstacklocation)设置 IRP 堆栈位置指针。 然后，调用[ **IoGetCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetcurrentirpstacklocation)获得到其自己在驱动程序创建 IRP 的 I/O 堆栈位置的指针并将启动后设置状态以供其自身[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)例程。

4.  调用[ **IoGetNextIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetnextirpstacklocation)获得到下一步低驱动程序的 I/O 在驱动程序创建 IRP 的堆栈位置的指针并将它设置为主要函数代码**IRP\_MJ\_SCSI**和 SRB (请参阅[存储类驱动程序](storage-class-drivers.md))。

5.  转换将数据传输到设备为特定于设备的、 使用了非标准格式如有必要。

6.  调用[ **IoSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutine)如果驱动程序分配任何内存，如通过调用 SRB、 SCSI 请求检测缓冲区、 MDL，和/或 IRP 内存[ **IoAllocateIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)或[ **IoBuildAsynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuildasynchronousfsdrequest)，或如果驱动程序必须转换数据从源中特定于设备的、 使用了非标准格式的设备。

7.  传递驱动程序创建 IRP 到 （和通过） 与下一步较低驱动程序[ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)。

## <a name="span-idhandlingsrbformatsspanspan-idhandlingsrbformatsspanspan-idhandlingsrbformatsspanhandling-srb-formats"></a><span id="Handling_SRB_formats"></span><span id="handling_srb_formats"></span><span id="HANDLING_SRB_FORMATS"></span>处理 SRB 格式


从 Windows 8 开始，在类驱动程序和端口驱动程序之间筛选 SFD 必须检查受支持的 SRB 格式。 具体而言，这涉及到检测 SRB 格式和正确访问结构的成员。 在 IRP SRB 是[ **SCSI\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block) and 或[**存储\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_storage_request_block). 筛选器驱动程序可以确定提前通过发出以下端口驱动程序支持哪些 Srb [ **IOCTL\_存储\_查询\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_query_property)请求并指定**StorageAdapterProperty**标识符。 **SrbType**并**AddressType**中返回的值[**存储\_适配器\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_adapter_descriptor)结构表示 SRB 格式和端口驱动程序所使用的寻址方案。 任何新 Srb 分配和发送的筛选器驱动程序必须是类型的由查询返回。

同样，从 Windows 8 开始，支持仅的 Srb SFDs [ **SCSI\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block)必须检查的类型**SrbType**中返回值[**存储\_适配器\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_adapter_descriptor)结构设置为**SRB\_类型\_SCSI\_请求\_阻止**。 若要处理这种情况时**SrbType**设置为**SRB\_类型\_存储\_请求\_阻止**相反，必须设置筛选器驱动程序为完成例程[ **IOCTL\_存储\_查询\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_query_property)时**StorageAdapterProperty**在其上的驱动程序发送的请求中设置标识符。 在完成例程**SrbType**中的成员**存储\_适配器\_描述符**修改为**SRB\_类型\_SCSI\_请求\_阻止**正确设置受支持的类型。

下面是一个筛选器调度例程用于处理这两种 SRB 格式的示例。

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

## <a name="span-idsettinguprequestsspanspan-idsettinguprequestsspanspan-idsettinguprequestsspansetting-up-requests"></a><span id="Setting_up_requests"></span><span id="setting_up_requests"></span><span id="SETTING_UP_REQUESTS"></span>设置请求


存储类驱动程序，如可能拥有 SFD *BuildRequest*或*SplitTransferRequest*例程以从驱动程序的调用*调度*例程，或可能会实现相同的功能内联。

有关详细信息*BuildRequest*并*SplitTransferRequest*例程，请参阅[存储类驱动程序](storage-class-drivers.md)。 有关的常规要求的详细信息*调度*例程，请参阅[写入调度例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/writing-dispatch-routines)。

 

 




