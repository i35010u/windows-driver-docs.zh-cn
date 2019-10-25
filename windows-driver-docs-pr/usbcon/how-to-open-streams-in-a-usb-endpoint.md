---
Description: 本主题讨论静态流功能，并说明 USB 客户端驱动程序如何在 USB 3.0 设备的大容量终结点中打开和关闭流。
title: 如何打开和关闭 USB 大容量终结点中的静态流
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0797008cf70cafb5a82485cad8be7f81ce0a9b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844392"
---
# <a name="how-to-open-and-close-static-streams-in-a-usb-bulk-endpoint"></a>如何打开和关闭 USB 大容量终结点中的静态流


本主题讨论*静态流功能*，并说明 usb 客户端驱动程序如何在 usb 3.0 设备的大容量终结点中打开和关闭流。

在 USB 2.0 及更早版本的设备中，批量终结点可以通过终结点发送或接收单个数据流。 在 USB 3.0 设备中，批量终结点能够通过终结点发送和接收多个数据流。

Windows 8 中 Microsoft 提供的 USB 驱动程序堆栈支持多个流。 这使得客户端驱动程序能够将独立 i/o 请求发送到与 USB 3.0 设备中的批量终结点相关联的每个流。 不会序列化对不同流的请求。

对于客户端驱动程序，流表示具有相同特征集的多个逻辑端点。 若要向特定流发送请求，客户端驱动程序需要该流的句柄（类似于终结点的管道句柄）。 流 i/o 请求的 URB 类似于向大容量终结点发出 i/o 请求的 URB。 唯一的区别是管道句柄。 若要将 i/o 请求发送到流，驱动程序会指定流的管道句柄。

在设备配置过程中，客户端驱动程序将发送一个选择-配置请求，还可以选择一个选择接口请求。 这些请求将为在接口的活动设置中定义的终结点检索一组管道句柄。 对于支持流的终结点，终结点管道句柄可用于将 i/o 请求发送到*默认流*（第一个流），直到驱动程序打开流（接下来将讨论）。

如果客户端驱动程序要将请求发送到默认流之外的流，则驱动程序必须打开并获取所有流的句柄。 为此，客户端驱动程序通过指定要打开的流的数目来发送一个*打开流请求*。 使用流完成客户端驱动程序之后，驱动程序可以通过发送处理*结束请求*来选择关闭它们。

内核模式驱动程序框架（KMDF）不支持静态流本质。 客户端驱动程序必须发送 Windows 驱动模型（WDM）样式 URBs，以打开和关闭流。 本主题介绍如何设置这些 URBs 的格式并将其发送。 用户模式驱动程序框架（UMDF）-客户端驱动程序无法使用静态流功能。

本主题包含标记为**WDM 驱动程序**的一些注释。 这些说明介绍了需要发送流请求的基于 WDM 的 USB 客户端驱动程序的例程。

### <a name="prerequisites"></a>必备条件

在客户端驱动程序可以打开或关闭流之前，驱动程序必须具有：

- 称为[**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)方法。

  此方法要求客户端协定版本 USBD 客户端\_协定\_版本\_602\_。 通过指定该版本，客户端驱动程序必须遵守一组规则。 有关详细信息，请参阅[最佳做法：使用 URBs](usb-client-driver-contract-in-windows-8.md)。

  调用会检索框架的 USB 目标设备对象的 WDFUSBDEVICE 句柄。 为了对打开的流进行后续调用，需要该句柄。 通常，客户端驱动程序会在驱动程序的[**EVT_WDF_DEVICE_PREPARE_HARDWARE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)事件回调例程中注册自身。

  <strong>WDM 驱动程序： * * 调用[ </strong>USBD\_CreateHandle * *](<https://msdn.microsoft.com/library/windows/hardware/hh406241>)例程，并使用 USB 驱动程序堆栈获取驱动程序注册的 USBD 句柄。

- 配置了设备，并为支持流的大容量终结点获取了 WDFUSBPIPE 管道句柄。 若要获取管道句柄，请对所选配置中接口的当前替代设置调用[**WdfUsbInterfaceGetConfiguredPipe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredpipe)方法。

  \* * WDM 驱动程序： * * 通过发送选择配置或选择接口请求来获取 USBD 管道句柄。 有关详细信息，请参阅[如何为 USB 设备选择配置](how-to-select-a-configuration-for-a-usb-device.md)。

<a name="instructions"></a>说明
------------

### <a name="how-to-open-static-streams"></a>如何打开静态流

<a href="" id="open-streams"></a>
1. 通过调用[**WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)方法，确定基础 USB 驱动程序堆栈和主机控制器是否支持静态流功能。 通常，客户端驱动程序会在驱动程序的[**EVT_WDF_DEVICE_PREPARE_HARDWARE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)事件回调例程中调用例程。

   <strong>WDM 驱动程序： * * 调用[ </strong>USBD\_QueryUsbCapability<strong> ](<https://msdn.microsoft.com/library/windows/hardware/hh406230>)例程。通常，驱动程序会查询要在驱动程序的启动设备例程（[</strong>IRP\_MN\_START\_设备<strong>](<https://msdn.microsoft.com/library/windows/hardware/ff551749>)）中使用的功能。有关代码示例，请参阅 * * USBD\_QueryUsbCapability</strong>。

   提供以下信息：

   - 对[**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)的前一次调用中检索的 USB 设备对象的句柄，用于客户端驱动程序注册。

     <strong>WDM 驱动程序： * * 传递先前对 USBD\_CreateHandle * * 的调用中[</strong>检索到的 USBD 句柄](<https://msdn.microsoft.com/library/windows/hardware/hh406241>)。

     如果客户端驱动程序要使用特定功能，则驱动程序必须首先查询基础 USB 驱动程序堆栈，以确定驱动程序堆栈和主机控制器是否支持该功能。 如果支持此功能，则该驱动程序应发送请求以使用功能。 某些请求需要 URBs，例如流功能（如步骤5中所述）。 对于这些请求，请确保使用相同的句柄来查询功能和分配 URBs。 这是因为驱动程序堆栈使用句柄来跟踪驱动程序可以使用的支持的功能。

     例如，如果你获取了 USBD\_句柄（通过调用[**USBD\_CreateHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)），则通过调用[**USBD\_QueryUsbCapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))查询驱动程序堆栈，并通过调用[**URB\_USBD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)来分配 UrbAllocate。 在这两个调用中传递相同的 USBD\_句柄。

     如果调用 KMDF 方法[**WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)和[**WdfUsbTargetDeviceCreateUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)，请在这些方法调用中为框架目标对象指定相同的 WDFUSBDEVICE 句柄。

   - 分配给 GUID\_USB\_功能\_静态\_流的 GUID。
   - 输出缓冲区（指向 USHORT 的指针）。 完成后，缓冲区会用主机控制器支持的流的最大数目（每个终结点）填充。
   - 输出缓冲区的长度（以字节为单位）。 对于流，长度为 `sizeof (USHORT)`。

2. 计算返回的 NTSTATUS 值。 如果例程成功完成，则返回状态\_成功，支持静态流功能。 否则，该方法将返回相应的错误代码。
3. 确定要打开的流的数量。 可以打开的最大流数受以下限制：
   -   主机控制器支持的流的最大数目。 该数字由调用方提供的输出缓冲区中的[**WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability) （对于 WDM 驱动程序， [**USBD\_QueryUsbCapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))）接收。 Microsoft 提供的 USB 驱动程序堆栈最多支持255个流。 **WdfUsbTargetDeviceQueryUsbCapability**在计算流数时，会考虑到这一限制。 此方法从不返回大于255的值。
   -   设备中的终结点支持的最大流数。 若要获取该数字，请检查终结点伴随描述符（请参阅[**USB\_SUPERSPEED\_终结点\_伴随\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_superspeed_endpoint_companion_descriptor)中的 Usbspec）。 若要获取终结点伴随描述符，必须分析该配置描述符。 若要获取配置描述符，客户端驱动程序必须调用[**WdfUsbTargetDeviceRetrieveConfigDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)方法。 必须使用 helper 例程[**USBD\_ParseConfigurationDescriptorEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_parseconfigurationdescriptorex)和[**USBD\_ParseDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_parsedescriptors)。 有关代码示例，请参阅[如何枚举 USB 管道](how-to-get-usb-pipe-handles.md)中名为 RetrieveStreamInfoFromEndpointDesc 的示例函数。

   若要确定最大流数，请选择主机控制器和终结点支持的两个值中的较小者。
4. 分配包含*n*个元素的[**USBD\_流的数组\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_stream_information)结构，其中*n*是要打开的流的数目。 当驱动程序使用完流之后，客户端驱动程序负责释放此数组。
5. 通过调用[**WdfUsbTargetDeviceCreateUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)方法为打开流请求分配 URB。 如果调用成功完成，则该方法将检索 WDF 内存对象和由 USB 驱动程序堆栈分配的[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构的地址。

   <strong>WDM 驱动程序： * * 调用[ </strong>USBD\_UrbAllocate * *](<https://msdn.microsoft.com/library/windows/hardware/hh406250>)例程。

6. 为打开流请求设置 URB 的格式。 URB 使用[ **\_URB\_打开\_静态\_流**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_open_static_streams)结构来定义请求。 若要设置 URB 的格式，请执行以下操作：
   -   终结点的 USBD 管道句柄。 如果有一个 WDF 管道对象，则可以通过调用[**WdfUsbTargetPipeWdmGetPipeHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipewdmgetpipehandle)方法获取 USBD 管道句柄。
   -   流数组（在步骤4中创建）
   -   指向[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构的指针（在步骤5中创建）。

   若要设置 URB 的格式，请调用[**UsbBuildOpenStaticStreamsRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbbuildopenstaticstreamsrequest) ，并将所需信息作为参数值传递。 请确保指定给**UsbBuildOpenStaticStreamsRequest**的流数量不超过支持的最大流数量。
7. 通过调用[**WdfRequestSend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)方法将 URB 作为 WDF 请求对象发送。 若要同步发送请求，请改为调用[**WdfUsbTargetDeviceSendUrbSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)方法。

   \* * WDM 驱动程序： * * 将 URB 与 IRP 相关联，并将 IRP 提交到 USB 驱动程序堆栈。 有关详细信息，请参阅[如何提交 URB](send-requests-to-the-usb-driver-stack.md)。

8. 请求完成后，检查请求的状态。

   如果 USB 驱动程序堆栈未通过请求，URB 状态将包含相关错误代码。 "备注" 部分中介绍了一些常见的故障条件。

如果请求的状态（IRP 或 WDF 请求对象）指示 USBD\_状态\_成功，则表明请求已成功完成。 检查[**USBD\_流**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_stream_information)的数组，\_在完成时收到的信息结构。 数组中填充了所请求流的相关信息。 USB 驱动程序堆栈用流信息填充数组中的每个结构（例如，作为 USBD\_管道\_句柄接收的句柄）、流标识符和最大传输大小。 流现在可以传输数据。

对于打开流请求，需要分配一个 URB 和一个数组。 在打开的流请求完成之后，客户端驱动程序必须通过对关联的 WDF 内存对象调用[**WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)方法来释放 URB。 如果驱动程序通过调用[**WdfUsbTargetDeviceSendUrbSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)同步发送请求，则该方法在返回后必须释放 WDF 内存对象。 如果客户端驱动程序通过调用[**WdfRequestSend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)以异步方式发送请求，则驱动程序必须在与请求关联的驱动程序实现的完成例程中释放 WDF 内存对象。

流数组可在客户端驱动程序使用流完成后释放，或已将其存储为 i/o 请求。 在本主题中包含的代码示例中，驱动程序将流数组存储在设备上下文中。 在释放设备对象之前，驱动程序就会释放设备上下文。

### <a name="how-to-transfer-data-to-a-particular-stream"></a>如何将数据传输到特定流

若要将数据传输请求发送到特定流，你将需要一个 WDF 请求对象。 通常，客户端驱动程序不需要分配 WDF 请求对象。 当 i/o 管理器收到来自应用程序的请求时，i/o 管理器将为该请求创建 IRP。 该 IRP 会被框架截取。 然后，框架会分配一个 WDF 请求对象来表示 IRP。 然后，框架将 WDF 请求对象传递给客户端驱动程序。 然后，客户端驱动程序可将请求对象与数据传输 URB 相关联，并将其发送到 USB 驱动程序堆栈。

如果客户端驱动程序没有从框架接收 WDF 请求对象并希望以异步方式发送请求，则驱动程序必须通过调用[**WdfRequestCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreate)方法来分配 wdf 请求对象。 通过调用[**WdfUsbTargetPipeFormatRequestForUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforurb)来设置新对象的格式，并通过调用[**WdfRequestSend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)发送请求。

在同步情况下，传递 WDF 请求对象是可选的。

若要将数据传输到流，必须使用 URBs。 必须通过调用[**WdfUsbTargetPipeFormatRequestForUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforurb)来设置 URB 的格式。

流*不*支持以下 WDF 方法：

-   [**WdfUsbTargetPipeFormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforread)
-   [**WdfUsbTargetPipeFormatRequestForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforwrite)
-   [**WdfUsbTargetPipeReadSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipereadsynchronously)
-   [**WdfUsbTargetPipeWriteSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipewritesynchronously)

以下过程假定客户端驱动程序从框架接收 request 对象。

1.  通过调用[**WdfUsbTargetDeviceCreateUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)分配 URB。 此方法分配一个 WDF 内存对象，其中包含新分配的 URB。 客户端驱动程序可以选择为每个 i/o 请求分配一个 URB，或分配一个 URB 并将其用于同一类型的请求。
2.  通过调用[**UsbBuildInterruptOrBulkTransferRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbbuildinterruptorbulktransferrequest)为大容量传输设置 URB 的格式。 在*PipeHandle*参数中，指定流的句柄。 在以前的请求中获取了流句柄，如[如何打开静态流](#open-streams)部分中所述。
3.  通过调用[**WdfUsbTargetPipeFormatRequestForUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforurb)方法来设置 WDF 请求对象的格式。 在调用中，指定包含数据传输 URB 的 WDF 内存对象。 在步骤1中分配了内存对象。
4.  通过调用[**WdfRequestSend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)或[**WDFUSBTARGETPIPESENDURBSYNCHRONOUSLY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipesendurbsynchronously)，将 URB 作为 WDF 请求发送。 如果调用**WdfRequestSend**，则必须通过调用[**WdfRequestSetCompletionRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsetcompletionroutine)来指定完成例程，以便在异步操作完成时，客户端驱动程序可以获得通知。 必须在完成例程中释放数据传输 URB。

<strong>WDM 驱动程序： * * 通过调用[ </strong>USBD\_UrbAllocate<strong> ](<https://msdn.microsoft.com/library/windows/hardware/hh406250>)来分配一个 URB，并将其格式化以便[</strong>进行大容量传输（请参阅\_URB\_<strong>](<https://msdn.microsoft.com/library/windows/hardware/ff540352>)大容量\_或\_中断\_传输）。若要设置 URB 的格式，可以[</strong>手动<strong>](<https://msdn.microsoft.com/library/windows/hardware/ff538953>)调用 UsbBuildInterruptOrBulkTransferRequest 或设置 URB 结构的格式。在 URB 的 * * PipeHandle 成员中指定流的句柄</strong>。

### <a name="how-to-close-static-streams"></a>如何关闭静态流

驱动程序使用完后，客户端驱动程序可以关闭流。 但是，关闭流请求是可选的。 当取消配置与流相关联的终结点时，USB 驱动程序堆栈会关闭所有流。 如果选择了其他配置或接口、设备已删除等，则会取消对终结点的配置。 如果驱动程序要打开不同数量的流，则客户端驱动程序必须关闭流。 发送结束流请求：

1.  通过调用[**WdfUsbTargetDeviceCreateUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)来分配[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构。
2.  为关闭流请求设置 URB 的格式。 [**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构的**UrbPipeRequest**成员是[ **\_URB\_管道\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_pipe_request)结构。 填写其成员，如下所示：
    -   [ **\_URB\_PIPE\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_pipe_request)的**Hdr**成员必须是 URB\_函数\_关闭\_静态\_流
    -   **PipeHandle**成员必须是包含正在使用的打开流的终结点的句柄。

3.  通过调用[**WdfRequestSend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)或[**WDFUSBTARGETDEVICESENDURBSYNCHRONOUSLY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)，将 URB 作为 WDF 请求发送。

关闭句柄请求会关闭客户端驱动程序先前打开的所有流。 客户端驱动程序无法使用请求来关闭终结点中的特定流。

<a name="remarks"></a>备注
-------

**发送静态流请求的最佳实践**

USB 驱动程序堆栈对收到的 URB 执行多个验证。 若要避免验证错误，客户端驱动程序必须考虑以下事项：

-   不要向不支持流的终结点发送开放流或关闭流请求。 调用[**WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability) （适用于 WDM 驱动程序， [**USBD\_QueryUsbCapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))）来确定静态流支持，并仅在终结点支持时发送流请求。
-   不要请求超出所支持的最大流数的数量（流打开），或发送请求而不指定流数。 根据 USB 驱动程序堆栈和设备终结点支持的流数量确定流的数量。
-   不要向已打开流的终结点发送打开流请求。
-   不要将关闭流请求发送到没有打开的流的终结点。
-   为终结点打开静态流后，请不要通过使用通过选择配置或选择接口请求获取的终结点管道句柄来发送 i/o 请求。 即使静态流已关闭，也是如此。

**重置和中止管道操作**

有时，与终结点之间的传输可能会失败。 此类故障可能是由于终结点或主机控制器上的错误条件导致的，如延迟或暂停条件。 若要清除错误情况，客户端驱动程序首先取消挂起的传输，然后重置与终结点关联的管道。 若要取消挂起的传输，客户端驱动程序可以发送中止管道请求。 若要重置管道，客户端驱动程序必须发送重置管道请求。

对于流传输，不支持对与大容量终结点相关联的各个流进行中止管道和重置管道请求。 如果在特定的流管道上传输失败，则主机控制器停止对所有其他管道（适用于其他流）的传输。 若要从错误情况中恢复，客户端驱动程序应手动取消到每个流的传输。 然后，客户端驱动程序必须通过使用大容量终结点的管道句柄发送重置管道请求。 对于该请求，客户端驱动程序必须在[ **\_URB\_管道\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_pipe_request)结构中指定终结点的管道句柄，并将 URB 函数（**Hdr. function**）设置为 URB\_函数\_同步\_RESET\_管道\_和\_清楚\_卡住。

## <a name="complete-example"></a>完整示例


下面的代码示例演示如何打开流。

```cpp
NTSTATUS
    OpenStreams (
    _In_ WDFDEVICE Device,
    _In_ WDFUSBPIPE Pipe)
{
    NTSTATUS status;

    PDEVICE_CONTEXT deviceContext;

    PPIPE_CONTEXT pipeContext;

    USHORT cStreams = 0;

    USBD_PIPE_HANDLE usbdPipeHandle;

    WDFMEMORY urbMemory = NULL;
    PURB      urb = NULL;

    PAGED_CODE();

    deviceContext =GetDeviceContext(Device);

    pipeContext = GetPipeContext (Pipe);

    if (deviceContext->MaxStreamsController == 0)
    {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Static streams are not supported.");

        status = STATUS_NOT_SUPPORTED;

        goto Exit;

    }

    // If static streams are not supported, number of streams supported is zero. 

    if (pipeContext->MaxStreamsSupported == 0)
    {
        status = STATUS_DEVICE_CONFIGURATION_ERROR;

        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Static streams are not supported by the endpoint.");

        goto Exit;
    }

    // Determine the number of streams to open.
    // Compare the number of streams supported by the endpoint with the 
    // number of streams supported by the host controller, and choose the 
    // lesser of the two values. The deviceContext->MaxStreams value was 
    // obtained in a previous call to WdfUsbTargetDeviceQueryUsbCapability
    // that determined whether or not static streams is supported and
    // retrieved the maximum number of streams supported by the 
    // host controller. The device context stores the values for IN and OUT 
    // endpoints.

    // Allocate an array of USBD_STREAM_INFORMATION structures to store handles to streams.
    // The number of elements in the array is the number of streams to open.
    // The code snippet stores the array in its device context.


    cStreams = min(deviceContext->MaxStreamsController, pipeContext->MaxStreamsSupported);

    // Allocate an array of streams associated with the IN bulk endpoint
    // This array is released in CloseStreams.

    pipeContext->StreamInfo = (PUSBD_STREAM_INFORMATION) ExAllocatePoolWithTag (
        NonPagedPool,
        sizeof (USBD_STREAM_INFORMATION) * cStreams,
        USBCLIENT_TAG);

    if (pipeContext->StreamInfo == NULL)
    {
        status = STATUS_INSUFFICIENT_RESOURCES;

        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Could not allocate stream information array.");

        goto Exit;
    }

    RtlZeroMemory (pipeContext->StreamInfo,  
        sizeof (USBD_STREAM_INFORMATION) * cStreams);

    // Get USBD pipe handle from the WDF target pipe object. The client driver received the
    // endpoint pipe handles during device configuration.

    usbdPipeHandle = WdfUsbTargetPipeWdmGetPipeHandle (Pipe);


    // Allocate an URB for the open streams request. 
    // WdfUsbTargetDeviceCreateUrb returns the address of the 
    // newly allocated URB and the WDFMemory object that 
    // contains the URB.

    status = WdfUsbTargetDeviceCreateUrb (
        deviceContext->UsbDevice,
        NULL,
        &urbMemory,
        &urb);

    if (status != STATUS_SUCCESS)
    {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Could not allocate URB for an open-streams request.");

        goto Exit;
    }

    // Format the URB for the open-streams request.
    // The UsbBuildOpenStaticStreamsRequest inline function formats the URB by specifying the
    // pipe handle to the entire bulk endpoint, number of streams to open, and the array of stream structures.

    UsbBuildOpenStaticStreamsRequest (
        urb,
        usbdPipeHandle,
        (USHORT)cStreams,
        pipeContext->StreamInfo);


    // Send the request synchronously.
    // Upon completion, the USB driver stack populates the array of with handles to streams.

    status = WdfUsbTargetPipeSendUrbSynchronously (
        Pipe,
        NULL,
        NULL,
        urb);

    if (status != STATUS_SUCCESS)
    {
        goto Exit;
    }

Exit:

    if (urbMemory)
    {
        WdfObjectDelete (urbMemory);
    }

    return status;

}
```

## <a name="related-topics"></a>相关主题
[USB i/o 操作](usb-device-i-o.md)  



