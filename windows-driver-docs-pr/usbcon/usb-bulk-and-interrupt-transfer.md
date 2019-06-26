---
Description: 本主题提供有关 USB 批量传输的简要概述。
title: 如何将发送 USB 大容量传输请求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 173e34fbb1885aac2824d350341f7cbfe82a9dda
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368752"
---
# <a name="how-to-send-usb-bulk-transfer-requests"></a>如何将发送 USB 大容量传输请求


本主题提供有关 USB 批量传输的简要概述。 它还提供有关如何对客户端驱动程序可以发送和接收来自设备的大容量数据的分步说明。

-   [有关大容量终结点](#about-bulk-endpoints)
-   [大容量事务](#bulk-transactions)
-   [USB 大容量传输客户端驱动程序任务](#usb-client-driver-tasks-for-a-bulk-transfer)
-   [大容量传输请求示例](#bulk-transfer-request-example)
    -   [必备条件](#prerequisites)
    -   [步骤 1：获取传输缓冲区。](#step-1--get-the-transfer-buffer--)
    -   [步骤 2：格式化并将一个框架请求对象发送到 USB 驱动程序堆栈。](#step-2--format-and-send-a-framework-request-object-to-the-usb-driver-stack-)
    -   [步骤 3：实现请求的完成例程。](#step-3--implement-a-completion-routine-for-the-request-)

## <a name="about-bulk-endpoints"></a>有关大容量终结点


USB 大容量终结点可传输大量数据。 大容量传输量都是可靠的允许硬件错误检测，并且涉及有限的数量的硬件中的重试。 对于大容量终结点的传输，总线上不保留带宽。 当存在多个面向不同类型的终结点的传输请求时，控制器首次计划传输时间关键数据，如等时，中断数据包。 仅当未使用的带宽上有可用的总线，控制器计划大容量传输。 总线上没有任何其他大量的流量，大容量复制可能会快速。 但是，当在总线正忙于处理其他传输，大容量数据可以无限期等待。

下面是一个大容量终结点的主要功能：

-   大容量终结点是可选的。 它们都支持想要将大量数据传输的 USB 设备。 例如，将文件传输到闪存驱动器，或从打印机或扫描仪的数据。
-   USB 全速、 高速度、 和 SuperSpeed 设备支持大容量终结点。 低速度设备不支持大容量终结点。
-   终结点是单向的可以是数据传输 IN 或 OUT 方向。 大容量 IN 终结点用于读取数据从设备复制到的主机和输出终结点的大容量用于将数据从主机到设备发送。
-   终结点具有 CRC 位，以检查有错误，从而提供数据完整性。 CRC 错误自动转发数据。
-   SuperSpeed 大容量终结点可以支持流。 流允许主机以将传输发送到单个流管道。
-   大容量终结点的最大数据包大小取决于设备的总线速度。 有关完整的速度、 高速度、 和 SuperSpeed;最大数据包大小分别为 64，512 和 1024 个字节。

## <a name="bulk-transactions"></a>大容量事务


像所有其他 USB 传输，主机将始终启动大容量传输。 通信发生在主机和目标终结点之间。 USB 协议不会强制任何大容量事务中发送的数据格式。

总线上的通信的主机和设备的方式取决于设备的连接的速度。 本部分介绍高速度和显示主机和设备之间的通信的 SuperSpeed 大容量传输的一些示例。

可以使用任何 USB 分析器，例如小猎狗 Ellisys，LeCroy USB 协议分析器来查看事务和数据包的结构。 分析器设备显示了如何发送到或无法通过网络从 USB 设备接收数据。 在此示例中，让我们看一些由 LeCroy USB 分析器捕获的跟踪。 此示例是仅用于提供信息。 这并不代表 Microsoft 的认可。

**大容量出事务示例**

此分析器跟踪快速显示出事务示例将大容量。

![示例数据事务跟踪。](images/bulk-out-hs.png)

在前面的跟踪中，主机通过使用 PID 超时设置 （输出令牌） 发送令牌数据包来启动出传输到高速大容量终结点，大容量。 数据包包含设备和目标终结点的地址。 后带数据包中，主机发送数据包中包含大容量负载。 如果终结点接受传入的数据，它会发送 ACK 数据包。 在此示例中，我们可以看到主机发送到设备地址： 1; 31 个字节终结点地址：2.

如果在数据数据包到达时，不能接收数据时，该终结点正忙，设备可以发送 NAK 数据包。 在这种情况下，主机开始将 PING 数据包发送到设备。 只要设备未准备好接收数据，设备使用 NAK 数据包响应。 在设备准备就绪后，它会确认数据包。 主机可以恢复扩展传输。

此分析器跟踪举例说明 SuperSpeed 出事务的大容量。

![示例数据事务跟踪。](images/bulk-out.png)

在前面的跟踪中，主机通过发送数据的数据包将启动到 SuperSpeed 大容量终结点的扩展事务。 数据包包含大容量负载、 设备和终结点地址。 在此示例中，我们可以看到，主机将 31 个字节发送到设备地址： 4;终结点地址：2.

设备接收和确认数据包并返回到主机发送 ACK 数据包。 如果在数据数据包到达时，不能接收数据时，该终结点正忙，设备可以发送 NRDY 数据包。 与高速度、 不同后接收 NRDY 数据包中，主机不会反复轮询设备。 相反，主机会等待来自设备 ERDY。 在设备准备就绪后，它将发送 ERDY 数据包和主机然后可以将数据发送到终结点。

**在大容量事务示例**

此分析器跟踪快速显示示例大容量在事务。

![示例数据事务跟踪。](images/bulk-in-hs.png)

在前面的跟踪中，主机将通过发送令牌的数据包的 PID 为设置为在启动该事务 （在令牌中）。 设备会发送包含大容量负载的数据包。 如果终结点不没有发送任何数据或还未准备好发送数据，设备可以发送 NAK 握手数据包。 从设备收到 ACK 数据包之前，主机重试中传输。 该 ACK 数据包意味着该设备已接受数据。

此分析器跟踪显示示例 SuperSpeed 大容量在事务。

![示例数据事务跟踪。](images/bulk-in.png)

若要启动从 SuperSpeed 终结点的大容量中传输，主机通过发送 ACK 数据包来启动大容量事务。 USB 规范 3.0 版可优化传输此初始部分通过合并 ACK 和数据包中为一个确认数据包。 而不是在令牌中，对于 SuperSpeed，主机会发送要启动的大容量复制的确认令牌。 设备使用一个数据包进行响应。 然后，主机通过发送 ACK 数据包确认数据包。 如果终结点正忙，无法发送数据，设备可以发送 NRDY 的状态。 在这种情况下，主机的等待，直到它会从设备获取 ERDY 数据包。

## <a name="usb-client-driver-tasks-for-a-bulk-transfer"></a>USB 大容量传输客户端驱动程序任务


应用程序或在主机上的驱动程序始终启动大容量传输来发送或接收数据。 客户端驱动程序将请求提交到 USB 驱动程序堆栈。 USB 驱动程序堆栈到主控制器程序请求，然后协议数据包 （如在上一部分中所述） 通过网络向设备发送。

让我们看到客户端驱动程序将对于应用程序或另一个驱动程序的请求的结果的大容量传输请求的提交。 或者，驱动程序可以启动其自身上的传输。 而不考虑方法时，驱动程序必须具有的传输缓冲区和请求，以便初始化大容量复制。

对于 KMDF 驱动程序，请求一个框架请求对象中描述 (请参阅[WDF 请求对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/))。 客户端驱动程序通过指定要将请求发送到 USB 驱动程序堆栈的 WDFREQUEST 句柄调用请求对象的方法。 如果客户端驱动程序从应用程序或另一个驱动程序的请求响应中发送大容量传输，框架将创建一个请求对象和使用 framework 队列对象将请求传递到客户端驱动程序。 在这种情况下，客户端驱动程序可以将该请求用于发送大容量传输的目的。 如果客户端驱动程序启动的请求，该驱动程序可以选择要分配其自己的请求对象。

如果应用程序或另一个驱动程序发送或请求数据，则将传输缓冲区传递到驱动程序框架。 或者，客户端驱动程序可以分配传输缓冲区，并创建请求对象，如果驱动程序将启动其自身上的传输。

下面是客户端驱动程序的主要任务：

1.  获取传输缓冲区。
2.  获取格式，并将一个框架请求对象发送到 USB 驱动程序堆栈。
3.  实现完成例程，若要在 USB 驱动程序堆栈完成请求时获得通知。

本主题介绍这些任务使用驱动程序将在其中启动应用程序的请求的结果的大容量传输来发送或接收数据的一个示例。

若要从设备读取数据，客户端驱动程序可以使用提供持续的读取器对象的框架。 有关详细信息，请参阅[如何使用来从 USB 管道读取数据的连续读取器](how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md)。

## <a name="bulk-transfer-request-example"></a>大容量传输请求示例


请考虑的示例方案，应用程序要读取或写入数据到你的设备。 应用程序调用 Windows Api 来发送此类请求。 在此示例中，应用程序打开的句柄设备通过设备接口发布在内核模式驱动程序的 GUID。 然后，应用程序调用[ **ReadFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)或[ **WriteFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-writefile)启动读取或写入请求。 在该调用中，应用程序还可以指定包含要读取或写入的数据的缓冲区，该缓冲区的长度。

I/O 管理器接收请求，创建 I/O 请求数据包 (IRP)，并将其转发到客户端驱动程序。

框架截获的请求，创建一个框架请求对象，并将其添加到框架队列对象。 然后，框架会通知新的请求待处理的客户端驱动程序。 通知通过调用的驱动程序的队列回调例程[ *EvtIoRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)或[ *EvtIoWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)。

当框架提供给客户端驱动程序的请求时，它将接收这些参数：

-   包含请求的 framework 队列对象的句柄 WDFQUEUE。
-   WDFREQUEST 句柄的框架请求对象，包含有关此请求的详细信息。
-   传输长度，即，要读取或写入的字节数。

在客户端驱动程序的实现中的[ *EvtIoRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)或[ *EvtIoWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_write)，驱动程序会检查请求参数和可以根据需要执行验证检查。

如果使用 SuperSpeed 大容量终结点的流，你将 URB 中发送请求，因为 KMDF 本质上不支持流。 有关提交传输到流的大容量终结点的请求的信息，请参阅[如何打开和关闭 USB 大容量终结点中的静态流](how-to-open-streams-in-a-usb-endpoint.md)。

如果不使用流，可以使用 KMDF 定义方法来发送请求，如下面的过程中所述：

### <a name="prerequisites"></a>系统必备

在开始之前，请确保您知道此信息：

-   客户端驱动程序必须创建 framework USB 目标设备对象并通过调用获取 WDFUSBDEVICE 句柄[ **WdfUsbTargetDeviceCreateWithParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)方法。

    如果使用 Microsoft Visual Studio Professional 2012 使用提供的 USB 模板，模板代码执行这些任务。 模板代码获取目标设备对象的句柄，并将存储在设备上下文中。 详细信息，请参阅"设备源代码"中[了解 USB 客户端驱动程序代码结构 (KMDF)](understanding-the-kmdf-template-code-for-usb.md)。

-   WDFREQUEST 句柄的框架请求对象，包含有关此请求的详细信息。
-   要读取或写入的字节数。
-   与目标终结点相关联的 framework 管道对象 WDFUSBPIPE 句柄。 您必须先获取管道句柄在设备配置过程中由枚举管道。 有关详细信息，请参阅[如何枚举 USB 管道](how-to-get-usb-pipe-handles.md)。

    如果大容量终结点支持流，必须具有到流处理的管道。 有关详细信息，请参阅[如何打开和关闭 USB 大容量终结点中的静态流](how-to-open-streams-in-a-usb-endpoint.md)。

### <a href="" id="step-1--get-the-transfer-buffer--"></a>步骤 1:获取传输缓冲区。

传输缓冲区或传输缓冲区 MDL 包含要发送或接收的数据。 本主题假定你在发送或接收的传输缓冲区中的数据。 传输缓冲区 WDF 内存对象中所述 (请参阅[WDF 内存对象引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/))。 若要获取与传输缓冲区关联的内存对象，调用这些方法之一：

-   对于大容量传输请求中，调用[ **WdfRequestRetrieveOutputMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)方法。
-   对于大容量传输请求，调用[ **WdfRequestRetrieveInputMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)方法。

客户端驱动程序不需要来释放此内存。 与父请求对象相关联和发布父时释放内存。

### <a href="" id="step-2--format-and-send-a-framework-request-object-to-the-usb-driver-stack-"></a>步骤 2:格式化并将一个框架请求对象发送到 USB 驱动程序堆栈。

以异步还是同步，可以发送传输请求。

以下是异步方法：

-   [**WdfUsbTargetPipeFormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforread)
-   [**WdfUsbTargetPipeFormatRequestForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforwrite)

此列表中的方法设置请求的格式。 如果异步发送请求，请将指针设置为驱动程序实现完成例程通过调用[ **WdfRequestSetCompletionRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine)方法 （下一步中所述）。 若要发送请求，调用[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)方法。

如果以同步方式发送请求，调用这些方法：

-   [**WdfUsbTargetPipeReadSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipereadsynchronously)
-   [**WdfUsbTargetPipeWriteSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipewritesynchronously)

有关代码示例，请参阅这些方法的参考主题的示例部分。
### <a href="" id="step-3--implement-a-completion-routine-for-the-request-"></a>步骤 3:实现请求的完成例程。

如果以异步方式发送请求，则必须实现完成例程，若要在 USB 驱动程序堆栈完成请求时获得通知。 完成后，框架调用驱动程序的完成例程。 该框架将传递这些参数：

-   请求对象的句柄 WDFREQUEST。
-   请求的 I/O 目标对象的句柄 WDFIOTARGET。
-   一个指向[ **WDF\_请求\_完成\_PARAMS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/ns-wdfrequest-_wdf_request_completion_params)结构，其中包含完成信息。 特定于 USB 的信息包含在**CompletionParams-&gt;Parameters.Usb**成员。
-   该驱动程序对其调用中指定的上下文的 WDFCONTEXT 句柄[ **WdfRequestSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine)。

在完成例程中，执行以下任务：

-   通过获取检查请求的状态**CompletionParams-&gt;IoStatus.Status**值。
-   检查 USB 驱动程序堆栈设置 USBD 状态。
-   如果管道出错，执行错误恢复操作。 有关详细信息，请参阅[如何从 USB 管道错误中恢复](how-to-recover-from-usb-pipe-errors.md)。
-   检查传输的字节数。

    当请求的字节数已传输到或从设备时，大容量传输已完成。 如果通过调用 KMDF 方法发送请求缓冲区，则请检查在获得的值**CompletionParams-&gt;Parameters.Usb.Completion-&gt;Parameters.PipeWrite.Length**或**CompletionParams-&gt;Parameters.Usb.Completion-&gt;Parameters.PipeRead.Length**成员。

    在简单传输 USB 驱动程序堆栈在一个包中发送所有请求的字节数的位置，可以检查比较**长度**值与请求的字节数。 如果 USB 驱动程序堆栈传输多个数据包中的请求，您必须跟踪的传输的字节数和剩余的字节数。

-   如果已传输的总字节数，完成请求。 如果出现错误条件，完成请求，返回的错误代码。 完成请求，通过调用[ **WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)方法。 如果你想要设置信息，例如传输的字节数，请调用[ **WdfRequestCompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff549945withinformation)。
-   请确保完成请求的信息后，字节数必须为等于或小于请求的字节数。 框架验证这些值。 如果长度中设置已完成的请求是大于原始请求长度，可能会出现 bugcheck。

此示例代码演示如何客户端驱动程序可以提交的大容量传输请求。 驱动程序设置完成例程。 下一步的代码块中演示了该例程。

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

此示例代码显示了大容量传输完成例程实现。 客户端驱动程序完成完成例程中的请求，并设置此请求的信息： 传输状态和字节数。

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
[USB I/O 传输](usb-device-i-o.md)  
[如何打开和关闭 USB 大容量终结点中的静态流](how-to-open-streams-in-a-usb-endpoint.md)  



