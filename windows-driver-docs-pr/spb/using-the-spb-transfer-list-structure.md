---
title: 将 SPB_TRANSFER_LIST 结构用于自定义 IOCTL
description: 如果简单外围总线（SPB）控制器驱动程序支持一个或多个自定义 i/o 控制（IOCTL）请求，请使用 SPB_TRANSFER_LIST 结构来描述这些请求中的读取和写入缓冲区。
ms.assetid: 577122CC-D1F8-41C5-BE77-A22FC8516B82
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db2c5048a1d3c0ad49e880f31d57a5bfc6bddc30
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839619"
---
# <a name="using-the-spb_transfer_list-structure-for-custom-ioctls"></a>使用 SPB\_为自定义 IOCTLs 传输\_列表结构


如果简单外围总线（SPB）控制器驱动程序支持一个或多个自定义 i/o 控制（IOCTL）请求，请使用[**SPB\_传输\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spb/ns-spb-spb_transfer_list)结构来描述这些请求中的读取和写入缓冲区。 此结构提供了一种统一的方法来描述请求中的缓冲区，并避免与方法\_的缓冲 i/o 操作相关联的缓冲区复制开销。

如果自定义 IOCTL 请求使用**SPB\_传输\_列表**结构，则 SPB 控制器驱动程序必须调用[**SpbRequestCaptureIoOtherTransferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbrequestcaptureioothertransferlist)方法，以便在请求的进程上下文中捕获这些缓冲区发出. 驱动程序可以调用[**SpbRequestGetTransferParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbrequestgettransferparameters)方法来访问这些缓冲区。

[**Ioctl\_spb\_完整\_双工**](https://msdn.microsoft.com/library/windows/hardware/hh974774)和[**IOCTL\_SPB\_执行**](https://msdn.microsoft.com/library/windows/hardware/hh450857)定义为[spb i/o 请求接口](https://docs.microsoft.com/previous-versions/hh698224(v=vs.85))一部分的\_序列请求，使用**spb\_传输 @no__** 用于描述其读取和写入缓冲区的 T_13_ 列表结构。 **Spb\_传输**IOCTL\_SPB\_列表结构 **\_完全\_双工**请求同时描述请求中的写入缓冲区和读取缓冲区（按该顺序）。 **Spb\_传输**IOCTL\_SPB\_列表结构 **\_EXECUTE\_序列**请求可描述任意序列的读取和写入缓冲区。

同样，你可以将自定义 IOCTLs 定义为要求其**SPB\_传输\_列表**结构以使用某个读和写缓冲区的组合，并在列表中指定可能需要的任何缓冲区顺序。

用于 SPB 外围设备的内核模式 Driver Foundation （KMDF）驱动程序将调用一个方法（如[**WdfIoTargetSendIoctlSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously) ），将 IOCTL 请求发送到 SPB 控制器。 此方法具有*InputBuffer*和*OutputBuffer*参数。 对于某些类型的设备，驱动程序可能会将这两个参数分别指向写入缓冲区和读取缓冲区，以用于 IOCTL 请求。 但是，若要向 SPB 控制器发送 IOCTL 请求，则 SPB 外围设备驱动程序将*InputBuffer*参数设置为指向\_列表结构中指向 SPB 的内存描述符 **\_传输**。 此结构描述 i/o 控制操作所需的任何读取或写入缓冲区。 驱动程序将*OutputBuffer*参数设置为 NULL。

同样，用于 SPB 外围设备的用户模式 Driver Foundation （UMDF）驱动程序将调用方法（如[**IWDFIoTarget：： FormatRequestForIoctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl) ）来格式化 i/o 控制操作的 i/o 请求。 此方法具有*pInputMemory*和*pOutputMemory*参数。 某些类型的设备的驱动程序可能使用这两个参数来指向写入缓冲区，并为 IOCTL 请求读取缓冲区。 但是，若要向 SPB 控制器发送 IOCTL 请求，则 SPB 外围设备驱动程序将*pInputMemory*参数设置为指向包含**SPB\_传输\_列表**结构的内存对象。 此结构描述 i/o 控制操作所需的任何读取或写入缓冲区。 驱动程序将*pOutputMemory*参数设置为 NULL。

## <a name="parameter-checking-and-buffer-capture"></a>参数检查和缓冲区捕获


当 SPB framework 扩展（SpbCx）接收到**IOCTL\_SPB\_执行\_序列**请求时，SpbCx 会通过调用驱动程序的[*EvtSpbControllerIoSequence*](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_sequence)函数将此请求传递给 SPB 控制器驱动程序。 在此调用之前，SpbCx 将检查**SPB\_传输**描述请求中的缓冲区\_列表结构。 SpbCx 捕获请求发起方的进程上下文中的这些缓冲区。 （只能在分配内存的进程中访问用户模式内存中的缓冲区。）此外，SpbCx 检查请求中的参数值是否有效。

当 SpbCx 收到**IOCTL\_SPB\_完整\_双工**请求或自定义 IOCTL 请求时，SpbCx 会通过调用驱动程序的[*EvtSpbControllerIoOther*](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_other)回调函数将此请求传递到 SPB 控制器驱动程序。 在进行此调用之前，SpbCx 不会对请求中的参数值进行验证检查，也不会在发起方的上下文中捕获请求的缓冲区。 针对这些请求的参数检查和缓冲区捕获是 SPB 控制器驱动程序的责任。

如果 SPB 控制器驱动程序支持**IOCTL\_SPB\_完整\_双工**请求，或支持使用**SPB\_传输\_列表**结构的任何自定义 ioctl 请求，则驱动程序必须实现一个[*EvtIoInCallerContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)回调函数。 驱动程序在对注册驱动程序的*EvtSpbControllerIoOther*回调函数的[**SpbControllerSetIoOtherCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbcontrollersetioothercallback)方法的调用中提供了一个指向此函数的指针作为输入参数。 当 SpbCx 收到**IOCTL\_SPB\_完整\_双工**请求或自定义 IOCTL 请求时，SpbCx 将在发起方的上下文中调用该驱动程序的*EvtIoInCallerContext*函数。 如果 IOCTL 请求使用**SPB\_传输\_列表**结构，则*EvtIoInCallerContext*函数将调用[**SpbRequestCaptureIoOtherTransferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbrequestcaptureioothertransferlist)方法来捕获请求中的缓冲区。 *EvtIoInCallerContext*函数还可能执行请求的一些初步处理。

下面的代码示例演示一个由 SPB 控制器驱动程序实现的*EvtIoInCallerContext*函数。

```cpp
VOID
EvtIoInCallerContext(
    _In_  WDFDEVICE   SpbController,
    _In_  WDFREQUEST  FxRequest
    ) 
{
    NTSTATUS status = STATUS_SUCCESS;
    WDF_REQUEST_PARAMETERS fxParams;
  
    WDF_REQUEST_PARAMETERS_INIT(&fxParams);
    WdfRequestGetParameters(FxRequest, &fxParams);

    if ((fxParams.Type != WdfRequestTypeDeviceControl) &&
        (fxParams.Type != WdfRequestTypeDeviceControlInternal))
    {
        status = STATUS_NOT_SUPPORTED;
        goto exit;
    }

    //
    // The driver should check for custom IOCTLs that it handles.
    // If the IOCTL is not recognized, complete the request with a
    // status of STATUS_NOT_SUPPORTED.
    //

    switch (fxParams.Parameters.DeviceIoControl.IoControlCode)
    {
        ...

    default:
        status = STATUS_NOT_SUPPORTED;
        goto exit;
    }

    //
    // The IOCTL is recognized. Capture the buffers in the request.
    //

    status = SpbRequestCaptureIoOtherTransferList((SPBREQUEST)FxRequest);

    //
    // If the capture fails, the driver must complete the request instead
    // of placing it in the SPB controller's request queue.
    //

    if (!NT_SUCCESS(status))
    {
        goto exit;
    }

    status = WdfDeviceEnqueueRequest(SpbController, FxRequest);

    if (!NT_SUCCESS(status))
    {
        goto exit;
    }

exit:

    if (!NT_SUCCESS(status))
    {
        WdfRequestComplete(FxRequest, status);
    }
}
```

在上面的代码示例中， **switch**语句验证请求是否包含 SPB 控制器驱动程序识别的 IOCTL。 （为简洁起见，不显示**switch**语句的主体。）接下来，对**SpbRequestCaptureIoOtherTransferList**方法的调用捕获请求中的缓冲区。 如果此调用成功，则会将请求添加到 SPB 控制器的 i/o 队列。 否则，请求将以错误状态代码完成。

有关显示*EvtSpbControllerIoOther*函数的参数检查的[代码示例](https://docs.microsoft.com/windows-hardware/drivers/spb/handling-ioctl-spb-full-duplex-requests#code-example)，请参阅[处理**IOCTL\_SPB\_FULL\_双工**请求](https://docs.microsoft.com/windows-hardware/drivers/spb/handling-ioctl-spb-full-duplex-requests)。

 

 




