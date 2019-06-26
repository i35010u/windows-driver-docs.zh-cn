---
title: 将 SPB_TRANSFER_LIST 结构用于自定义 IOCTL
description: 如果您的简单外围总线 （存储） 控制器驱动程序支持一个或多个自定义的 I/O 控制 (IOCTL) 请求，使用 SPB_TRANSFER_LIST 结构描述读取和写入缓冲区中这些请求。
ms.assetid: 577122CC-D1F8-41C5-BE77-A22FC8516B82
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47fc55613b702f848d12368e434e9f19b2c1c8a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383494"
---
# <a name="using-the-spbtransferlist-structure-for-custom-ioctls"></a>使用存储\_传输\_的自定义 Ioctl 列表结构


如果您的简单外围总线 （存储） 控制器驱动程序支持一个或多个自定义的 I/O 控制 (IOCTL) 请求，使用[**存储\_传输\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spb/ns-spb-spb_transfer_list)结构来描述读取和写入缓冲区中这些请求。 此结构提供了统一的方式来描述在请求中，缓冲区，可避免复制缓冲区的开销与方法关联\_缓冲 I/O 操作。

如果自定义 IOCTL 请求使用**存储\_传输\_列表**结构，您的存储控制器驱动程序必须调用[ **SpbRequestCaptureIoOtherTransferList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nf-spbcx-spbrequestcaptureioothertransferlist)方法来捕获这些缓冲区的请求发起方进程上下文中。 您的驱动程序可以调用[ **SpbRequestGetTransferParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nf-spbcx-spbrequestgettransferparameters)方法来访问这些缓冲区。

[ **IOCTL\_存储\_完整\_双工**](https://msdn.microsoft.com/library/windows/hardware/hh974774)并[ **IOCTL\_存储\_EXECUTE\_序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857)作为的一部分定义的请求[存储 I/O 请求接口](https://docs.microsoft.com/previous-versions/hh698224(v=vs.85))，使用**存储\_传输\_列表**结构来描述其读取和写入缓冲区。 **存储\_传输\_列表**结构**IOCTL\_存储\_完整\_双工**请求描述写入缓冲区和在请求中读取的缓冲区 （按此顺序）。 **存储\_传输\_列表**结构**IOCTL\_存储\_EXECUTE\_序列**请求可以描述的任意序列的读取和写入缓冲区。

同样，可以定义需要您自定义 Ioctl 他们**存储\_传输\_列表**结构结合的读取和写入缓冲区，并指定任何排序的列表中的缓冲区的可能还需要。

存储外围设备的内核模式驱动程序的基础 (KMDF) 驱动程序调用的方法，如[ **WdfIoTargetSendIoctlSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously)将 IOCTL 请求发送到存储控制器。 此方法具有*InputBuffer*并*OutputBuffer*参数。 对于某些类型的设备驱动程序可能会使用这两个参数以指向写入缓冲区并读取缓冲区，分别为 IOCTL 请求。 但是，若要将 IOCTL 请求发送到的存储控制器，存储外围设备驱动程序集*InputBuffer*参数以指向指向的内存描述符**存储\_传输\_列表**结构。 此结构描述任何读取或写入缓冲区所需的 I/O 控制操作。 驱动程序集*OutputBuffer*参数为 NULL。

同样，存储外围设备的用户模式驱动程序的基础 (UMDF) 驱动程序调用的方法如[ **IWDFIoTarget::FormatRequestForIoctl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl)格式化 I/O 控制的 I/O 请求操作。 此方法具有*pInputMemory*并*pOutputMemory*参数。 对于某些类型的设备驱动程序可能会使用这两个参数以指向写入缓冲区并读取 IOCTL 请求的缓冲区。 但是，若要将 IOCTL 请求发送到的存储控制器，存储外围设备驱动程序集*pInputMemory*参数，以对内存对象，其中包含指向**存储\_传输\_列表**结构。 此结构描述任何读取或写入缓冲区所需的 I/O 控制操作。 驱动程序集*pOutputMemory*参数为 NULL。

## <a name="parameter-checking-and-buffer-capture"></a>参数检查和缓冲区捕获


当存储框架扩展 (SpbCx) 收到**IOCTL\_存储\_EXECUTE\_序列**请求，SpbCx 此将请求传递给存储控制器驱动程序通过调用在驱动程序[ *EvtSpbControllerIoSequence* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nc-spbcx-evt_spb_controller_sequence)函数。 此调用前检查 SpbCx**存储\_传输\_列表**结构，描述在请求中的缓冲区。 SpbCx 捕获这些缓冲区的请求发起方进程上下文中。 （在用户模式内存中的缓冲区可以访问仅在分配内存的进程中。）此外，SpbCx 检查请求中的参数值是否有效。

当收到 SpbCx **IOCTL\_存储\_完整\_双工**IOCTL 请求或自定义请求，SpbCx 此将请求传递给存储控制器驱动程序通过调用驱动程序的[ *EvtSpbControllerIoOther* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nc-spbcx-evt_spb_controller_other)回调函数。 进行此调用之前, SpbCx 不验证检查的参数值在请求中，并不会捕获上下文中的原始发件人请求的缓冲区。 这些请求的参数检查和缓冲区捕获的存储控制器驱动程序负责。

如果存储控制器驱动程序支持**IOCTL\_存储\_完整\_双工**请求，也支持使用任何自定义 IOCTL 请求**存储\_传输\_列表**结构针对其缓冲区，该驱动程序必须实现[ *EvtIoInCallerContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)回调函数。 驱动程序作为输入参数对的调用中提供此函数的指针[ **SpbControllerSetIoOtherCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nf-spbcx-spbcontrollersetioothercallback)注册驱动程序的方法*EvtSpbControllerIoOther*回调函数。 当收到 SpbCx **IOCTL\_存储\_完整\_双工**IOCTL 请求或自定义请求，SpbCx 调用驱动程序的*EvtIoInCallerContext*中的函数发起方的上下文。 如果使用 IOCTL 请求**存储\_传输\_列表**结构*EvtIoInCallerContext*函数调用[ **SpbRequestCaptureIoOtherTransferList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nf-spbcx-spbrequestcaptureioothertransferlist)方法来捕获在请求中的缓冲区。 *EvtIoInCallerContext*函数也可以执行一些初步处理请求。

下面的代码示例演示*EvtIoInCallerContext*由存储控制器驱动程序实现的函数。

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

在前面的代码示例中，**切换**语句验证该请求包含存储控制器驱动程序识别 IOCTL。 (为简洁起见，正文**切换**语句不会显示。)下一步，将会调用**SpbRequestCaptureIoOtherTransferList**方法捕获在请求中的缓冲区。 如果此调用成功，将请求添加到存储控制器的 I/O 队列。 否则，在请求完成，错误状态代码。

有关[的代码示例](https://docs.microsoft.com/windows-hardware/drivers/spb/handling-ioctl-spb-full-duplex-requests#code-example)显示参数检查*EvtSpbControllerIoOther*函数中，请参阅[处理**IOCTL\_存储\_完整\_双工**请求](https://docs.microsoft.com/windows-hardware/drivers/spb/handling-ioctl-spb-full-duplex-requests)。

 

 




