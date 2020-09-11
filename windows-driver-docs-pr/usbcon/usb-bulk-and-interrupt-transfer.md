---
description: 本主题提供有关 USB 批量传输的简要概述。
title: 如何将发送 USB 大容量传输请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73bad559d4c4d66be4ea9d67b002c956f519b18a
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009993"
---
# <a name="how-to-send-usb-bulk-transfer-requests"></a>如何将发送 USB 大容量传输请求


本主题提供有关 USB 批量传输的简要概述。 它还提供了有关客户端驱动程序如何从设备发送和接收大容量数据的分步说明。

-   [关于大容量终结点](#about-bulk-endpoints)
-   [大容量事务](#bulk-transactions)
-   [用于批量传输的 USB 客户端驱动程序任务](#usb-client-driver-tasks-for-a-bulk-transfer)
-   [批量传输请求示例](#bulk-transfer-request-example)
    -   [先决条件](#prerequisites)
    -   [步骤1：获取传输缓冲区。](#step-1--get-the-transfer-buffer--)
    -   [步骤2：设置框架请求对象的格式并将其发送到 USB 驱动程序堆栈。](#step-2--format-and-send-a-framework-request-object-to-the-usb-driver-stack-)
    -   [步骤3：为请求实现完成例程。](#step-3--implement-a-completion-routine-for-the-request-)

## <a name="about-bulk-endpoints"></a>关于大容量终结点


USB 大容量终结点可传输大量数据。 大容量传输可靠，允许硬件错误检测，并涉及硬件的重试次数限制。 为了传输到大容量终结点，总线上没有保留带宽。 如果有多个传输请求针对不同类型的终结点，则控制器将首先计划传输时间关键数据（例如，同步和中断数据包）。 只有当总线上没有未使用的带宽时，控制器才能计划大容量传输。 如果在总线上没有其他重要流量，则大容量传输速度会很快。 但是，当总线忙于其他传输时，大容量数据可能会无限期等待。

大容量终结点的主要功能如下：

-   大容量终结点是可选的。 它们受要传输大量数据的 USB 设备支持。 例如，将文件传输到闪存驱动器、从打印机或扫描仪传入或传出数据。
-   USB 全速、高速和 SuperSpeed 设备支持大容量终结点。 低速设备不支持大容量终结点。
-   终结点是单向的，数据可以按进出方向传输。 Bulk IN endpoint 用于将数据从设备读入主机，并使用 bulk 终结点将数据从主机发送到设备。
-   终结点有 CRC 位用于检查错误，从而提供数据完整性。 对于 CRC 错误，将自动重新传输数据。
-   SuperSpeed 大容量终结点可以支持流。 流允许主机向单独的流管道发送传输。
-   大容量终结点的最大数据包大小取决于设备的总线速度。 对于全速、高速和 SuperSpeed，最大数据包大小分别为64、512和1024字节。

## <a name="bulk-transactions"></a>大容量事务


与所有其他 USB 传输一样，主机始终启动大容量传输。 通信发生在主机和目标终结点之间。 USB 协议不会对在大容量事务中发送的数据强制使用任何格式。

主机和设备在总线上的通信方式取决于设备连接的速度。 本部分介绍了显示主机和设备之间通信的高速和 SuperSpeed 批量传输的一些示例。

可以使用任何 USB 分析器（例如 Beagle、Ellisys、LeCroy USB 协议分析器）来查看事务和数据包的结构。 分析器设备显示如何通过线路将数据发送到 USB 设备或从其接收数据。 在此示例中，让我们检查由 LeCroy USB 分析器捕获的某些跟踪。 此示例仅供参考， 不表示 Microsoft 的认可。

**批量输出事务示例**

此分析器跟踪高速显示一个示例大容量事务。

![示例数据事务的跟踪。](images/bulk-out-hs.png)

在前面的跟踪中，主机会通过将 PID 设置为 OUT (OUT token) 发送令牌数据包，来发起向高速大容量终结点的批量传输。 数据包包含设备和目标终结点的地址。 在输出数据包之后，主机将发送包含大容量有效负载的数据包。 如果终结点接受传入的数据，则会发送 ACK 数据包。 在此示例中，我们可以看到主机向设备地址发送了31个字节： 1;终结点地址：2。

如果在数据包到达时终结点处于繁忙状态，并且无法接收数据，则设备可以发送 NAK 数据包。 在这种情况下，主机会开始将 PING 数据包发送到设备。 只要设备尚未准备好接收数据，设备就会响应 NAK 的数据包。 设备准备就绪后，会使用 ACK 数据包进行响应。 然后，主机可以恢复传出传输。

此分析器跟踪显示一个 SuperSpeed bulk transaction 示例。

![示例数据事务的跟踪。](images/bulk-out.png)

在前面的跟踪中，主机通过发送数据包对 SuperSpeed 大容量终结点发起 OUT transaction。 数据包包含批量有效负载、设备和终结点地址。 在此示例中，我们可以看到主机向设备地址发送了31个字节： 4;终结点地址：2。

设备接收并确认数据包，并将 ACK 数据包发送回主机。 如果在数据包到达时终结点处于繁忙状态，并且无法接收数据，则设备可以发送 NRDY 数据包。 与高速不同，接收 NRDY 数据包后，主机不会重复轮询设备。 相反，主机会等待设备的 ERDY。 当设备准备就绪时，它会发送 ERDY 数据包，主机随后可以将数据发送到终结点。

**批量传入事务示例**

此分析器跟踪快速显示了事务中的一个示例。

![示例数据事务的跟踪。](images/bulk-in-hs.png)

在前面的跟踪中，主机将通过在令牌)  (中发送 PID 设置为的令牌数据包来启动该事务。 然后，设备将使用大容量有效负载发送数据包。 如果该终结点没有要发送的数据或尚未准备好发送数据，则该设备可以发送 NAK 握手数据包。 主机会重试传入传输，直至接收到设备收到的 ACK 数据包为止。 该 ACK 数据包表示设备已接受数据。

此分析器跟踪显示了事务中大容量的示例 SuperSpeed。

![示例数据事务的跟踪。](images/bulk-in.png)

若要从 SuperSpeed 终结点批量启动批量传输，主机会通过发送 ACK 数据包来启动大容量事务。 USB 规范版本3.0 通过将 ACK 和 IN 数据包合并为一个 ACK 数据包来优化传输的初始部分。 对于 SuperSpeed，主机发送确认令牌来启动大容量传输，而不是 IN 令牌。 设备使用数据包来做出响应。 然后，主机通过发送 ACK 数据包来确认数据包。 如果终结点处于繁忙状态且无法发送数据，则设备可以发送 NRDY 状态。 在这种情况下，主机会等待，直到从设备获取 ERDY 数据包。

## <a name="usb-client-driver-tasks-for-a-bulk-transfer"></a>用于批量传输的 USB 客户端驱动程序任务


主机上的应用程序或驱动程序始终启动大容量传输来发送或接收数据。 客户端驱动程序将请求提交到 USB 驱动程序堆栈。 USB 驱动程序堆栈会将请求发送到主机控制器，然后按照前面部分) 通过线路连接到设备中所述，将协议数据包 (。

让我们看看客户端驱动程序如何提交批量传输请求，这是因为应用程序或其他驱动程序的请求。 或者，驱动程序可以自行启动传输。 不管采用哪种方法，驱动程序都必须有传输缓冲区和请求，才能启动大容量传输。

对于 KMDF 驱动程序，请求在框架请求对象中进行了描述 (参阅 [WDF Request Object Reference](/windows-hardware/drivers/ddi/wdfrequest/)) 。 客户端驱动程序通过指定 WDFREQUEST 句柄来调用请求对象的方法，以将请求发送到 USB 驱动程序堆栈。 如果客户端驱动程序发送大容量传输来响应来自应用程序或另一个驱动程序的请求，则该框架将创建一个请求对象，并使用框架队列对象将该请求传递给客户端驱动程序。 在这种情况下，客户端驱动程序可能会出于发送大容量传输的目的使用该请求。 如果客户端驱动程序启动了请求，则驱动程序可以选择分配其自己的请求对象。

如果应用程序或其他驱动程序发送或请求的数据，则传输缓冲区将由框架传递给驱动程序。 或者，如果驱动程序自行启动传输，则客户端驱动程序可以分配传输缓冲区并创建 request 对象。

下面是客户端驱动程序的主要任务：

1.  获取传输缓冲区。
2.  获取、格式化框架请求对象并将其发送到 USB 驱动程序堆栈。
3.  实现完成例程，以便在 USB 驱动程序堆栈完成请求时获得通知。

本主题通过使用一个示例来说明这些任务，在此示例中，由于应用程序发送或接收数据的请求，该驱动程序将启动批量传输。

若要从设备中读取数据，客户端驱动程序可以使用框架提供的连续读取器对象。 有关详细信息，请参阅 [如何使用连续读取器读取 USB 管道中的数据](how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md)。

## <a name="bulk-transfer-request-example"></a>批量传输请求示例


请考虑一个示例方案，其中应用程序需要在设备中读取或写入数据。 应用程序调用 Windows Api 来发送此类请求。 在此示例中，应用程序使用内核模式下驱动程序发布的设备接口 GUID 打开设备的句柄。 然后，应用程序调用 [**ReadFile**](/windows/desktop/api/fileapi/nf-fileapi-readfile) 或 [**WriteFile**](/windows/desktop/api/fileapi/nf-fileapi-writefile) 以启动读取或写入请求。 在该调用中，应用程序还指定一个包含要读取或写入的数据的缓冲区以及该缓冲区的长度。

I/o 管理器接收请求，创建 (IRP) 的 i/o 请求数据包，并将其转发到客户端驱动程序。

框架截获请求，创建框架请求对象，并将其添加到框架队列对象。 然后，框架会通知客户端驱动程序，新请求正在等待处理。 该通知是通过调用 [*EvtIoRead*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read) 或 [*EvtIoWrite*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)的驱动程序的队列回调例程来完成的。

当框架将请求传递给客户端驱动程序时，它会收到以下参数：

-   包含请求的框架队列对象的 WDFQUEUE 句柄。
-   包含有关此请求的详细信息的 framework 请求对象的 WDFREQUEST 句柄。
-   传输长度，即要读取或写入的字节数。

在客户端驱动程序的 [*EvtIoRead*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read) 或 [*EvtIoWrite*](/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)实现中，驱动程序将检查请求参数，并且可以选择执行验证检查。

如果你使用 SuperSpeed 大容量终结点的流，则会在 URB 中发送请求，因为 KMDF 不支持流。 有关提交传输到大容量终结点流的请求的信息，请参阅 [如何在 USB 大容量终结点中打开和关闭静态流](how-to-open-streams-in-a-usb-endpoint.md)。

如果使用的不是流，则可以使用 KMDF 定义的方法发送请求，如以下过程中所述：

### <a name="prerequisites"></a>先决条件

在开始之前，请确保你具有以下信息：

-   客户端驱动程序必须已创建框架 USB 目标设备对象，并通过调用 [**WdfUsbTargetDeviceCreateWithParameters**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters) 方法获取了 WDFUSBDEVICE 句柄。

    如果使用 Microsoft Visual Studio Professional 2012 随附的 USB 模板，则模板代码会执行这些任务。 模板代码会获取目标设备对象的句柄并将其存储在设备上下文中。 有关详细信息，请参阅[了解 USB 客户端驱动程序代码结构 (KMDF)](understanding-the-kmdf-template-code-for-usb.md) 中的“设备源代码”。

-   包含有关此请求的详细信息的 framework 请求对象的 WDFREQUEST 句柄。
-   要读取或写入的字节数。
-   与目标终结点关联的框架管道对象的 WDFUSBPIPE 句柄。 你必须在设备配置过程中通过枚举管道获取管道句柄。 有关详细信息，请参阅 [如何枚举 USB 管道](how-to-get-usb-pipe-handles.md)。

    如果大容量终结点支持流，则必须具有流的管道句柄。 有关详细信息，请参阅 [如何在 USB 大容量终结点中打开和关闭静态流](how-to-open-streams-in-a-usb-endpoint.md)。

### <a name="step-1-get-the-transfer-buffer"></a><a href="" id="step-1--get-the-transfer-buffer--"></a>步骤1：获取传输缓冲区。

传输缓冲区或传输缓冲区 MDL 包含要发送或接收的数据。 本主题假设你要在传输缓冲区中发送或接收数据。 在 WDF 内存对象中介绍了传输缓冲区 (参阅 [Wdf Memory Object Reference](/windows-hardware/drivers/ddi/wdfmemory/)) 。 若要获取与传输缓冲区关联的内存对象，请调用以下方法之一：

-   对于批量传入请求，请调用 [**WdfRequestRetrieveOutputMemory**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory) 方法。
-   对于批量输出传输请求，请调用 [**WdfRequestRetrieveInputMemory**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory) 方法。

客户端驱动程序不需要释放此内存。 内存与父 request 对象相关联，并在释放父请求时释放。

### <a name="step-2-format-and-send-a-framework-request-object-to-the-usb-driver-stack"></a><a href="" id="step-2--format-and-send-a-framework-request-object-to-the-usb-driver-stack-"></a>步骤2：设置框架请求对象的格式并将其发送到 USB 驱动程序堆栈。

可以异步或同步发送传输请求。

以下是异步方法：

-   [**WdfUsbTargetPipeFormatRequestForRead**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforread)
-   [**WdfUsbTargetPipeFormatRequestForWrite**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforwrite)

此列表中的方法格式请求。 如果以异步方式发送请求，请通过调用 [**WdfRequestSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine) 方法来设置指向驱动程序实现的完成例程的指针， () 的下一步中所述。 若要发送请求，请调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 方法。

如果同步发送请求，请调用以下方法：

-   [**WdfUsbTargetPipeReadSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipereadsynchronously)
-   [**WdfUsbTargetPipeWriteSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipewritesynchronously)

有关代码示例，请参阅这些方法的参考主题的 "示例" 部分。
### <a name="step-3-implement-a-completion-routine-for-the-request"></a><a href="" id="step-3--implement-a-completion-routine-for-the-request-"></a>步骤3：为请求实现完成例程。

如果请求是异步发送的，则必须实现完成例程，以便在 USB 驱动程序堆栈完成请求时获得通知。 完成后，框架将调用驱动程序的完成例程。 框架传递以下参数：

-   Request 对象的 WDFREQUEST 句柄。
-   请求的 i/o 目标对象的 WDFIOTARGET 句柄。
-   一个指针，指向包含完成信息的 [**WDF \_ 请求 \_ 完成 \_ 参数**](/windows-hardware/drivers/ddi/wdfrequest/ns-wdfrequest-_wdf_request_completion_params) 结构。 USB 特定的信息包含在 CompletionParams 成员 ** &gt; ** 中。
-   WDFCONTEXT 在对 [**WdfRequestSetCompletionRoutine**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine)的调用中指定的上下文的句柄。

在完成例程中，执行以下任务：

-   通过获取 **CompletionParams- &gt; IoStatus** 值检查请求的状态。
-   检查 USB 驱动程序堆栈设置的 USBD 状态。
-   如果出现管道错误，请执行错误恢复操作。 有关详细信息，请参阅 [如何从 USB 管道中恢复错误](how-to-recover-from-usb-pipe-errors.md)。
-   检查传输的字节数。

    当请求的字节数已传入或传出设备时，将完成批量传输。 如果通过调用 KMDF 方法发送请求缓冲区，请检查在 CompletionParams 中收到的值 ** &gt; 。 &gt; PipeWrite** 或 CompletionParams 成员的值。- ** &gt; &gt; PipeRead.** 的成员。

    在 USB 驱动程序堆栈发送一个数据包中所有请求的字节的简单传输中，可以选中 "将 **长度** 值与请求的字节数进行比较"。 如果 USB 驱动程序堆栈传输多个数据包中的请求，则必须跟踪传输的字节数和剩余字节数。

-   如果传输的总字节数，请完成该请求。 如果出现错误条件，请完成请求并返回错误代码。 通过调用 [**WdfRequestComplete**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) 方法来完成请求。 如果要设置信息，例如传输的字节数，请调用 [**WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549945withinformation)。
-   请确保当你完成包含信息的请求时，字节数必须等于或小于请求的字节数。 框架将验证这些值。 如果完成的请求中设置的 length 大于原始请求长度，则会发生错误检测。

此代码示例演示客户端驱动程序如何提交批量传输请求。 驱动程序设置完成例程。 该例程显示在下一个代码块中。

```cpp
/*++

Routine Description:

This routine sends a bulk write request to the 
USB driver stack. The request is sent asynchronously and 
the driver gets notified through a completion routine.

Arguments:

Queue - Handle to a framework queue object.
Request - Handle to the framework request object.
Length - Number of bytes to transfer.


Return Value:

VOID

--*/


VOID Fx3EvtIoWrite(
    IN WDFQUEUE  Queue,
    IN WDFREQUEST  Request,
    IN size_t  Length
    )
{
    NTSTATUS  status;
    WDFUSBPIPE  pipe;
    WDFMEMORY  reqMemory;
    PDEVICE_CONTEXT  pDeviceContext;

    pDeviceContext = GetDeviceContext(WdfIoQueueGetDevice(Queue));

    pipe = pDeviceContext->BulkWritePipe;

    status = WdfRequestRetrieveInputMemory(
                                           Request,
                                           &reqMemory
                                           );
    if (!NT_SUCCESS(status))
    {
        goto Exit;
    }

    status = WdfUsbTargetPipeFormatRequestForWrite(
                                                   pipe,
                                                   Request,
                                                   reqMemory,
                                                   NULL
                                                   );
    if (!NT_SUCCESS(status))
       {
        goto Exit;
    }

    WdfRequestSetCompletionRoutine(
                                   Request,
                                   BulkWriteComplete,
                                   pipe
                                   );

    if (WdfRequestSend( Request,
                        WdfUsbTargetPipeGetIoTarget(pipe),
                        WDF_NO_SEND_OPTIONS) == FALSE) 
       {
        status = WdfRequestGetStatus(Request);
        goto Exit;
    }

Exit:
    if (!NT_SUCCESS(status)) {
        WdfRequestCompleteWithInformation(
                                          Request,
                                          status,
                                          0
                                          );
    }
    return;
}
```

此示例代码显示大容量传输的完成例程实现。 客户端驱动程序完成完成例程中的请求，并设置此请求信息：状态和传输的字节数。

```cpp
/*++

Routine Description:

This completion routine is invoked by the framework when
the USB drive stack completes the previously sent 
bulk write request. The client driver completes the 
the request if the total number of bytes were transferred
to the device.
In case of failure it queues a work item to start the 
error recovery by resetting the target pipe.

Arguments:

Queue - Handle to a framework queue object.
Request - Handle to the framework request object.
Length - Number of bytes to transfer.
Pipe - Handle to the pipe that is the target for this request.

Return Value:

VOID

--*/

VOID BulkWriteComplete(  
    _In_ WDFREQUEST                  Request,  
    _In_ WDFIOTARGET                 Target,  
    PWDF_REQUEST_COMPLETION_PARAMS   CompletionParams,  
    _In_ WDFCONTEXT                  Context  
    )  
{

    PDEVICE_CONTEXT deviceContext;

    size_t          bytesTransferred=0; 

    NTSTATUS        status;


    UNREFERENCED_PARAMETER (Target);
    UNREFERENCED_PARAMETER (Context);


    KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL, 
        "In completion routine for Bulk transfer.\n"));

    // Get the device context. This is the context structure that
    // the client driver provided when it sent the request.

    deviceContext = (PDEVICE_CONTEXT)Context;

    // Get the status of the request
    status = CompletionParams->IoStatus.Status;
    if (!NT_SUCCESS (status))
    {
        // Get the USBD status code for more information about the error condition.
        status = CompletionParams->Parameters.Usb.Completion->UsbdStatus;

        KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL,
            "Bulk transfer failed. 0x%x\n",  
            status));       

        // Queue a work item to start the reset-operation on the pipe
        // Not shown.

        goto Exit;
    }

    // Get the actual number of bytes transferred.
    bytesTransferred = 
            CompletionParams->Parameters.Usb.Completion->Parameters.PipeWrite.Length;

    KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL,
            "Bulk transfer completed. Transferred %d bytes. \n",  
            bytesTransferred));

Exit:

    // Complete the request and update the request with 
    // information about the status code and number of bytes transferred.

    WdfRequestCompleteWithInformation(Request, status, bytesTransferred);

    return;
}
```

## <a name="related-topics"></a>相关主题
[USB i/o 传输](usb-device-i-o.md)  
[如何打开和关闭 USB 大容量终结点中的静态流](how-to-open-streams-in-a-usb-endpoint.md)