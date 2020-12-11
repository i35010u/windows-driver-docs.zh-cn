---
title: 使用 USB 管道
description: 使用 USB 管道
keywords:
- framework 对象 WDK KMDF，USB 管道对象
- USB 管道 WDK KMDF
- 管道对象 WDK KMDF
- USB i/o 目标 WDK KMDF，USB 管道
- 连续读取器 WDK USB
- 重置管道 WDK KMDF
- 发送 URBs WDK KMDF
- USB 请求块 WDK KMDF
- URBs WDK KMDF
- 停止管道 WDK KMDF
- 写入管道 WDK KMDF
- 从管道中读取 WDK KMDF
- 输入管道 WDK KMDF
- 输出管道 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c943bf07636ed7b235a006f7e644b4b1bbcb211d
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97091082"
---
# <a name="working-with-usb-pipes"></a>使用 USB 管道


框架将 USB 接口中的每个管道表示为框架 USB 管道对象。 当驱动程序 [配置 USB 设备](working-with-usb-devices.md#selecting-a-device-configuration)时，框架会为每个选定接口中的每个管道创建一个框架 USB 管道对象。 通过管道对象方法，驱动程序可以执行以下操作：

-   [获取管道信息。](#obtaining-pipe-information)

-   [从管道读取。](#reading-from-a-pipe)

-   [写入管道。](#writing-to-a-pipe)

-   [停止或重置管道。](#stopping-and-resetting-a-pipe)

-   [将 URB 发送到管道。](#sending-a-urb-to-a-pipe)

### <a name="obtaining-pipe-information"></a><a href="" id="obtaining-pipe-information"></a> 获取管道信息

在调用 [**WdfUsbInterfaceGetConfiguredPipe**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredpipe) 以获取框架 USB 管道对象的句柄之后，驱动程序可以调用 usb 管道对象定义的以下方法来获取有关 usb 管道的信息：

<a href="" id="---------wdfusbtargetpipegetiotarget--------"></a>[**WdfUsbTargetPipeGetIoTarget**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegetiotarget)  
返回与 USB 管道关联的 i/o 目标对象的句柄。 驱动程序可以将此句柄传递给 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)。

<a href="" id="---------wdfusbtargetpipegetinformation--------"></a>[**WdfUsbTargetPipeGetInformation**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation)  
检索有关 USB 管道及其终结点的信息。

<a href="" id="---------wdfusbtargetpipegettype--------"></a>[**WdfUsbTargetPipeGetType**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegettype)  
返回 USB 管道的类型。

<a href="" id="---------wdfusbtargetpipeisinendpoint--------"></a>[**WdfUsbTargetPipeIsInEndpoint**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeisinendpoint)  
确定 USB 管道是否连接到输入终结点。

<a href="" id="---------wdfusbtargetpipeisoutendpoint--------"></a>[**WdfUsbTargetPipeIsOutEndpoint**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeisoutendpoint)  
确定 USB 管道是否连接到输出终结点。

<a href="" id="---------wdf-usb-pipe-direction-in--------"></a>[**WDF \_ USB \_ 管道 \_ 方向 \_**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_pipe_direction_in)  
确定 USB 终结点是否为输入终结点。

<a href="" id="---------wdf-usb-pipe-direction-out--------"></a>[**WDF \_ USB \_ 管道 \_ 方向 \_ 输出**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_pipe_direction_out)  
确定 USB 终结点是否为输出终结点。

有关相关信息，请参阅 [如何枚举 USB 管道](../usbcon/index.md)。

### <a name="reading-from-a-pipe"></a><a href="" id="reading-from-a-pipe"></a> 从管道读取

若要从 USB 输入管道中读取数据，驱动程序可以使用以下三种方法中的任何 (或全部) ：

-   同步读取数据

    若要从 USB 输入管道同步读取数据，驱动程序可以调用 [**WdfUsbTargetPipeReadSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipereadsynchronously) 方法。 此方法生成并发送读取请求，并在 i/o 操作完成后返回。

-   异步读取数据

    若要从 USB 输入管道异步读取数据，驱动程序可以调用 [**WdfUsbTargetPipeFormatRequestForRead**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforread) 方法来生成读取请求。 然后，该驱动程序可以调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 异步发送请求 (或同步) 。

-   异步和连续读取数据

    *连续的读取器* 是一个框架提供的机制，用于确保读取请求始终可用于 USB 管道。 此机制可保证驱动程序始终准备好从提供异步、未经请求的输入流的设备接收数据。 例如，网络接口卡 (NIC 的驱动程序) 可能使用连续读取器来接收输入数据。

    若要为输入管道配置连续读取器，驱动程序的 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 回调函数必须调用 [**WdfUsbTargetPipeConfigContinuousReader**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeconfigcontinuousreader) 方法。 此方法将一组读取请求排队给设备的 i/o 目标。

    此外，驱动程序的 [*EvtDeviceD0Entry*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) 回调函数必须调用 [**WdfIoTargetStart**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstart) 来启动持续读取器，驱动程序的 [*EvtDeviceD0Exit*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit) 回调函数必须调用 [**WdfIoTargetStop**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop) 以停止连续读取器。

    每次在设备上提供数据时，i/o 目标都将完成读取请求，并且框架将调用以下两个回调函数之一： [*EvtUsbTargetPipeReadComplete*](/windows-hardware/drivers/ddi/wdfusb/nc-wdfusb-evt_wdf_usb_reader_completion_routine)，如果 i/o 目标成功读取数据，则为 [*EvtUsbTargetPipeReadersFailed*](/windows-hardware/drivers/ddi/wdfusb/nc-wdfusb-evt_wdf_usb_readers_failed); 如果 i/o 目标报告错误，则为。

    如果未提供可选的 [*EvtUsbTargetPipeReadersFailed*](/windows-hardware/drivers/ddi/wdfusb/nc-wdfusb-evt_wdf_usb_readers_failed) 回调，则框架将通过发送另一个读取请求来响应失败的读取尝试。 因此，如果该总线处于不接受读取的状态，则该框架会持续发送新请求，以从失败的读取进行恢复。

    驱动程序调用 [**WdfUsbTargetPipeConfigContinuousReader**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeconfigcontinuousreader)之后，驱动程序不能使用 [**WdfUsbTargetPipeReadSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipereadsynchronously) 或 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 将 i/o 请求发送到管道，除非调用了驱动程序的 [*EvtUsbTargetPipeReadersFailed*](/windows-hardware/drivers/ddi/wdfusb/nc-wdfusb-evt_wdf_usb_readers_failed) 回调函数并返回 **FALSE**。

默认情况下，如果驱动程序指定的读取缓冲区不是管道的最大数据包大小的倍数，则框架将报告错误。 你的驱动程序可以调用 [**WdfUsbTargetPipeSetNoMaximumPacketSizeCheck**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipesetnomaximumpacketsizecheck) 来禁用此读取缓冲区大小测试。

如需相关信息，请参阅：

-   [如何将发送 USB 大容量传输请求](/windows-hardware/drivers/usbcon/usb-bulk-and-interrupt-transfer)
-   [如何将数据传输到 USB 常时等量终结点](/windows-hardware/drivers/usbcon/transfer-data-to-isochronous-endpoints)
-   [如何使用连续读取器从 USB 管道读取数据](../usbcon/index.md)

### <a name="writing-to-a-pipe"></a><a href="" id="writing-to-a-pipe"></a> 写入管道

若要将数据写入 USB 输出管道，你的驱动程序可以使用以下两种方法中的一种 () ：

-   同步写入数据

    若要将数据同步写入 USB 输出管道，驱动程序可以调用 [**WdfUsbTargetPipeWriteSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipewritesynchronously) 方法。 此方法生成并发送写入请求，并在 i/o 操作完成后返回。

-   异步写入数据

    若要以异步方式将数据写入 USB 输入管道，驱动程序可以调用 [**WdfUsbTargetPipeFormatRequestForWrite**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforwrite) 方法来生成写入请求。 然后，驱动程序可以调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 来异步发送请求。

有关相关信息，请参阅 [如何发送 USB 批量传输请求](/windows-hardware/drivers/usbcon/usb-bulk-and-interrupt-transfer)。

### <a name="stopping-and-resetting-a-pipe"></a><a href="" id="stopping-and-resetting-a-pipe"></a> 停止和重置管道

驱动程序可以调用以下方法来停止或重置 USB 管道：

<a href="" id="---------wdfusbtargetpipeabortsynchronously--------"></a>[**WdfUsbTargetPipeAbortSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeabortsynchronously)  
同步发送请求以停止 USB 管道。

<a href="" id="---------wdfusbtargetpipeformatrequestforabort--------"></a>[**WdfUsbTargetPipeFormatRequestForAbort**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforabort)  
格式化停止 USB 管道的请求。 驱动程序可以调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 来同步或异步发送请求。

<a href="" id="---------wdfusbtargetpiperesetsynchronously--------"></a>[**WdfUsbTargetPipeResetSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpiperesetsynchronously)  
同步发送请求以重置 USB 管道。

<a href="" id="---------wdfusbtargetpipeformatrequestforreset--------"></a>[**WdfUsbTargetPipeFormatRequestForReset**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforreset)  
格式化用于重置 USB 管道的请求。 驱动程序必须调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 以同步或异步发送请求。

如果驱动程序的 USB 目标 [完成](completing-i-o-requests.md) 的 i/o 请求带有错误状态值，则驱动程序应执行以下操作：

1.  如果目标尚未完成请求，请停止管道，并取消驱动程序已发送到 USB 目标的任何其他 i/o 请求。

    调用 [**WdfIoTargetStop**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop) ，并设置 [**WdfIoTargetCancelSentIo**](/windows-hardware/drivers/ddi/wdfiotarget/ne-wdfiotarget-_wdf_io_target_sent_io_action) 标志。

2.  将中止请求同步发送到管道。

    调用 [**WdfUsbTargetPipeAbortSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeabortsynchronously)，或调用 [**WdfUsbTargetPipeFormatRequestForAbort**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforabort) ，并将 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 与 [**WDF \_ 请求 \_ 发送 \_ 选项 \_ 同步**](/windows-hardware/drivers/ddi/wdfrequest/ns-wdfrequest-_wdf_request_send_options) 标志集一起调用。

3.  以同步方式将重置请求发送到管道。

    调用 [**WdfUsbTargetPipeResetSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpiperesetsynchronously)，或调用 [**WdfUsbTargetPipeFormatRequestForReset**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforreset) ，并将 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 与 [**WDF \_ 请求 \_ 发送 \_ 选项 \_ 同步**](/windows-hardware/drivers/ddi/wdfrequest/ns-wdfrequest-_wdf_request_send_options) 标志集一起调用。

4.  重新启动管道。

    调用 [**WdfIoTargetStart**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstart)。

5.  重新发送失败的 i/o 请求，以及按照失败请求的所有 i/o 请求。

出现大量多个故障之后，驱动程序应通过执行以下操作尝试重置 USB 端口：

1.  如果目标尚未完成，请停止所有活动管道，并取消驱动程序发送到每个管道的 USB 目标的任何其他 i/o 请求。

    对于每个活动管道，请调用 [**WdfIoTargetStop**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop) 并设置 [**WdfIoTargetCancelSentIo**](/windows-hardware/drivers/ddi/wdfiotarget/ne-wdfiotarget-_wdf_io_target_sent_io_action) 标志。

2.  同步发送请求以重置 USB 端口。

    调用 [**WdfUsbTargetDeviceResetPortSynchronously**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceresetportsynchronously)。

3.  重新启动管道。

    为驱动程序停止的每个管道调用 [**WdfIoTargetStart**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstart) 。

4.  重新发送失败的最后一个 i/o 请求，以及失败请求之后的所有 i/o 请求。

有关相关信息，请参阅 [如何从 USB 管道中恢复错误](../usbcon/index.md)。

### <a name="sending-an-urb-to-a-pipe"></a><a href="" id="sending-a-urb-to-a-pipe"></a> 向管道发送 URB

如果 KMDF 驱动程序通过发送 i/o 请求（包含 URBs）与 USB 管道通信，则驱动程序可以调用以下方法：

<a href="" id="---------wdfusbtargetpipesendurbsynchronously--kmdf-only-"></a>[**WdfUsbTargetPipeSendUrbSynchronously (KMDF 仅)**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipesendurbsynchronously)  
同步发送包含 URB 的 i/o 请求。

<a href="" id="---------wdfusbtargetpipeformatrequestforurb--kmdf-only-"></a>[**WdfUsbTargetPipeFormatRequestForUrb (KMDF 仅)**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforurb)  
设置包含 URB 的 i/o 请求的格式。 驱动程序可以调用 [**WdfRequestSend**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend) 来同步或异步发送请求。

<a href="" id="---------wdfusbtargetpipewdmgetpipehandle--kmdf-only-"></a>[**WdfUsbTargetPipeWdmGetPipeHandle (KMDF 仅)**](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipewdmgetpipehandle)  
返回设备的 USBD 管道句柄。 一些 URBs 需要此句柄。

 

