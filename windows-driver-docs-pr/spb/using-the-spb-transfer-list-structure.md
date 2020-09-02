---
title: 将 SPB_TRANSFER_LIST 结构用于自定义 IOCTL
description: 如果你的简单外围总线 (SPB) 控制器驱动程序支持一个或多个自定义 i/o 控件 (IOCTL) 请求，请使用 SPB_TRANSFER_LIST 结构来描述这些请求中的读取和写入缓冲区。
ms.assetid: 577122CC-D1F8-41C5-BE77-A22FC8516B82
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0310d27718c6c6461cef0a236b0d194d69404367
ms.sourcegitcommit: c766ab74e32eb44795cbbd1a4f352d3a6a9adc14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89389583"
---
# <a name="using-the-spb_transfer_list-structure-for-custom-ioctls"></a>使用 \_ \_ 自定义 IOCTLS 的 SPB 传输列表结构


如果你的简单外围总线 (SPB) 控制器驱动程序支持一个或多个自定义 i/o 控件 (IOCTL) 请求，请使用 [**SPB \_ 传输 \_ 列表**](/windows-hardware/drivers/ddi/spb/ns-spb-spb_transfer_list) 结构来描述这些请求中的读取和写入缓冲区。 此结构提供了一种统一的方法来描述请求中的缓冲区，并避免与方法缓冲 i/o 操作相关的缓冲区复制开销 \_ 。

如果自定义 IOCTL 请求使用 **SPB \_ 传输 \_ 列表** 结构，则 SPB 控制器驱动程序必须调用 [**SpbRequestCaptureIoOtherTransferList**](/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbrequestcaptureioothertransferlist) 方法，以便在请求发起方的进程上下文中捕获这些缓冲区。 驱动程序可以调用 [**SpbRequestGetTransferParameters**](/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbrequestgettransferparameters) 方法来访问这些缓冲区。

[**Ioctl \_ spb \_ \_ **](https://msdn.microsoft.com/library/windows/hardware/hh974774)全双工和[**ioctl \_ Spb \_ 执行 \_ 序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857)请求（定义为[SPB I/o 请求接口](/previous-versions/hh698224(v=vs.85))的一部分），请使用**spb \_ 传输 \_ 列表**结构描述它们的读取和写入缓冲区。 **IOCTL \_ spb \_ 全双工 \_ **请求的**SPB \_ 传输 \_ 列表**结构描述了写入缓冲区和读取缓冲区 (按顺序在请求中) 。 **IOCTL \_ spb \_ 执行 \_ 序列**请求的**SPB \_ 传输 \_ 列表**结构可描述任意序列的读取和写入缓冲区。

同样，你可以定义自定义 IOCTLs 以要求其 **SPB \_ 传输 \_ 列表** 结构使用某种类型的读取和写入缓冲区，并在列表中指定可能需要的任何缓冲区顺序。

用于 SPB 外围设备的内核模式驱动程序基础 (KMDF) 驱动程序调用诸如 [**WdfIoTargetSendIoctlSynchronously**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously) 的方法，将 IOCTL 请求发送到 SPB 控制器。 此方法具有 *InputBuffer* 和 *OutputBuffer* 参数。 对于某些类型的设备，驱动程序可能会将这两个参数分别指向写入缓冲区和读取缓冲区，以用于 IOCTL 请求。 但是，若要将 IOCTL 请求发送到 SPB 控制器，则 SPB 外围设备驱动程序将 *InputBuffer* 参数设置为指向用于指向 **spb \_ 传输 \_ 列表** 结构的内存描述符。 此结构描述 i/o 控制操作所需的任何读取或写入缓冲区。 驱动程序将 *OutputBuffer* 参数设置为 NULL。

同样，适用于 SPB 外围设备的用户模式驱动程序基础 (UMDF) 驱动程序调用方法，例如 [**IWDFIoTarget：： FormatRequestForIoctl**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl) ，以格式化 i/o 控制操作的 i/o 请求。 此方法具有 *pInputMemory* 和 *pOutputMemory* 参数。 某些类型的设备的驱动程序可能使用这两个参数来指向写入缓冲区，并为 IOCTL 请求读取缓冲区。 但是，若要向 SPB 控制器发送 IOCTL 请求，则 SPB 外围设备驱动程序将 *pInputMemory* 参数设置为指向包含 **SPB \_ 传输 \_ 列表** 结构的内存对象。 此结构描述 i/o 控制操作所需的任何读取或写入缓冲区。 驱动程序将 *pOutputMemory* 参数设置为 NULL。

## <a name="parameter-checking-and-buffer-capture"></a>参数检查和缓冲区捕获


当 (SpbCx) 的 SPB 框架扩展接收 **IOCTL \_ SPB \_ 执行 \_ 序列** 请求时，SpbCx 会通过调用驱动程序的 [*EvtSpbControllerIoSequence*](/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_sequence) 函数将此请求传递到 SPB 控制器驱动程序。 在此调用之前，SpbCx 会检查描述请求中的缓冲区的 **SPB \_ 传输 \_ 列表** 结构。 SpbCx 捕获请求发起方的进程上下文中的这些缓冲区。 用户模式内存中 (缓冲区只能在分配内存的进程中进行访问。 ) 另外，SpbCx 检查请求中的参数值是否有效。

当 SpbCx 收到 **IOCTL \_ SPB \_ 全双工 \_ ** 请求或自定义 ioctl 请求时，SpbCx 会通过调用驱动程序的 [*EvtSpbControllerIoOther*](/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_other) 回调函数将此请求传递给 SPB 控制器驱动程序。 在进行此调用之前，SpbCx 不会对请求中的参数值进行验证检查，也不会在发起方的上下文中捕获请求的缓冲区。 针对这些请求的参数检查和缓冲区捕获是 SPB 控制器驱动程序的责任。

如果 SPB 控制器驱动程序支持 **IOCTL \_ SPB \_ 全双工 \_ ** 请求，或支持任何对其缓冲区使用 **SPB \_ 传输 \_ 列表** 结构的自定义 IOCTL 请求，则驱动程序必须实现 [*EvtIoInCallerContext*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context) 回调函数。 驱动程序在对注册驱动程序的*EvtSpbControllerIoOther*回调函数的[**SpbControllerSetIoOtherCallback**](/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbcontrollersetioothercallback)方法的调用中提供了一个指向此函数的指针作为输入参数。 当 SpbCx 收到 **IOCTL \_ SPB \_ 全双工 \_ ** 请求或自定义 ioctl 请求时，SpbCx 将在发起方的上下文中调用该驱动程序的 *EvtIoInCallerContext* 函数。 如果 IOCTL 请求使用了 **SPB \_ 传输 \_ 列表** 结构，则 *EvtIoInCallerContext* 函数将调用 [**SpbRequestCaptureIoOtherTransferList**](/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbrequestcaptureioothertransferlist) 方法来捕获请求中的缓冲区。 *EvtIoInCallerContext*函数还可能执行请求的一些初步处理。

下面的代码示例演示一个由 SPB 控制器驱动程序实现的 *EvtIoInCallerContext* 函数。

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

在上面的代码示例中， **switch** 语句验证请求是否包含 SPB 控制器驱动程序识别的 IOCTL。  (为简洁起见，不显示 **switch** 语句的主体。 ) 接下来，对 **SpbRequestCaptureIoOtherTransferList** 方法的调用捕获请求中的缓冲区。 如果此调用成功，则会将请求添加到 SPB 控制器的 i/o 队列。 否则，请求将以错误状态代码完成。

有关显示 *EvtSpbControllerIoOther* 函数的参数检查的代码示例，请参阅 [处理 **IOCTL \_ SPB \_ 全双工 \_ ** 请求](./handling-ioctl-spb-full-duplex-requests.md)。

 

