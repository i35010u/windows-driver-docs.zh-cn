---
Description: This topic discusses static streams capability and explains how a USB client driver can open and close streams in a bulk endpoint of a USB 3.0 device.
title: 如何打开和关闭 USB 大容量终结点中的静态流
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e14aba7a384634b31fec0e4635c981c5005834d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562672"
---
# <a name="how-to-open-and-close-static-streams-in-a-usb-bulk-endpoint"></a>如何打开和关闭 USB 大容量终结点中的静态流


本主题讨论*静态流功能*并说明如何打开和关闭的流，大容量的 USB 3.0 设备终结点中 USB 客户端驱动程序。

在 USB 2.0 和更低版本设备，大容量终结点可以发送或接收单一数据流通过终结点。 在 USB 3.0 设备中大容量终结点具有的功能来发送和接收通过终结点的多个数据流。

在 Windows 8 中的由 Microsoft 提供的 USB 驱动程序堆栈支持多个流。 这使客户端驱动程序将独立的 I/O 请求发送到每个流与 USB 3.0 设备中的大容量终结点相关联。 将请求发送到不同的流不会序列化。

客户端驱动程序的流表示多个具有相同的特征集的逻辑终结点。 若要将请求发送到特定的流，客户端驱动程序需要该流的句柄 （类似于终结点的管道句柄）。 流 I/O 请求 URB 是类似于 URB 对大容量终结点的 I/O 请求。 唯一的区别是管道句柄。 若要将 I/O 请求发送到流，该驱动程序指定到流的管道句柄。

设备在配置期间，客户端驱动程序将发送一个选择配置的请求和 （可选） 选择接口请求。 这些请求检索管道句柄的接口活动设置中定义的终结点的集。 对于支持流终结点，可以使用终结点的管道句柄发送到的 I/O 请求到*默认流*（第一个流） 直到驱动程序打开流 （接下来将讨论）。

如果客户端驱动程序想要将请求发送到默认流以外的流，该驱动程序必须打开并获取句柄的所有流。 若要执行此操作，客户端驱动程序发送*打开流请求*通过指定要打开的流的数量。 驱动程序完成后在客户端使用流，该驱动程序可以根据需要来关闭它们发送*关闭流请求*。

内核模式驱动程序框架 (KMDF) 本质上不支持静态流。 客户端驱动程序必须发送 Windows 驱动程序模型 (WDM) 样式 URBs 的打开和关闭流。 本主题介绍如何发送这些 URBs 和格式。 用户模式驱动程序框架 (UMDF) 的客户端驱动程序不能使用静态流功能。

本主题包含标记为一些说明**WDM 驱动程序**。 这些说明描述了 WDM 基于 USB 的客户端驱动程序，想要发送流请求的例程。

### <a name="prerequisites"></a>先决条件

客户端驱动程序可以打开或关闭流之前，必须具有该驱动程序：

- 名为[ **WdfUsbTargetDeviceCreateWithParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh439428)方法。

  该方法要求客户端协定版本为 USBD\_客户端\_协定\_版本\_602。 通过指定该版本的客户端驱动程序必须遵守的一组规则。 有关详细信息，请参阅[最佳实践：使用 URBs](usb-client-driver-contract-in-windows-8.md)。

  该调用会检索 WDFUSBDEVICE 对象的句柄框架的 USB 目标设备。 该句柄所需执行后续调用以打开流。 通常情况下，在驱动程序的客户端驱动程序注册自身[ **EVT_WDF_DEVICE_PREPARE_HARDWARE** ](https://msdn.microsoft.com/library/windows/hardware/ff540880)事件回调例程。

  <strong>WDM 驱动程序: * * 调用[ </strong>USBD\_CreateHandle * *](<https://msdn.microsoft.com/library/windows/hardware/hh406241>)例程，并获取驱动程序的注册与 USB 驱动程序堆栈的 USBD 句柄。

- 配置设备和获取支持流的大容量终结点的 WDFUSBPIPE 管道句柄。 若要获取的管道句柄，请调用[ **WdfUsbInterfaceGetConfiguredPipe** ](https://msdn.microsoft.com/library/windows/hardware/ff550057)方法中所选配置的接口的当前备用设置。

  * * WDM 驱动程序: * * 通过发送选择配置或选择接口请求获取 USBD 管道句柄。 有关详细信息，请参阅[如何选择一种配置 USB 设备](how-to-select-a-configuration-for-a-usb-device.md)。

<a name="instructions"></a>说明
------------

### <a name="how-to-open-static-streams"></a>如何打开静态流

<a href="" id="open-streams"></a>
1. 确定基础的 USB 驱动程序堆栈主机控制器是否通过调用支持静态流功能[ **WdfUsbTargetDeviceQueryUsbCapability** ](https://msdn.microsoft.com/library/windows/hardware/hh439434)方法。 通常情况下，客户端驱动程序中的驱动程序调用例程[ **EVT_WDF_DEVICE_PREPARE_HARDWARE** ](https://msdn.microsoft.com/library/windows/hardware/ff540880)事件回调例程。

   <strong>WDM 驱动程序: * * 调用[ </strong>USBD\_QueryUsbCapability<strong> ](<https://msdn.microsoft.com/library/windows/hardware/hh406230>)例程。通常情况下，它想要使用的驱动程序的启动设备例程中的功能的驱动程序查询 ([</strong>IRP\_MN\_启动\_设备<strong>](<https://msdn.microsoft.com/library/windows/hardware/ff551749>))。有关代码示例中，请参阅 * * USBD\_QueryUsbCapability</strong>。

   提供以下信息：

   - 已检索，对上一个调用中的 USB 设备对象的句柄[ **WdfUsbTargetDeviceCreateWithParameters**](https://msdn.microsoft.com/library/windows/hardware/hh439428)，客户端驱动程序注册。

     <strong>WDM 驱动程序: * * 传递在上一调用检索到的 USBD 句柄[ </strong>USBD\_CreateHandle * *](<https://msdn.microsoft.com/library/windows/hardware/hh406241>)。

     如果客户端驱动程序想要使用的特殊功能，该驱动程序必须先查询基础的 USB 驱动程序堆栈，以确定驱动程序堆栈和主机控制器支持的功能。 如果支持该功能，则只有在此时，驱动程序应发送请求以使用的功能。 某些请求需要 URBs，如 （在步骤 5 中所述） 的流功能。 对于这些请求，请确保您使用的相同句柄的查询功能，并将配置 URBs。 这是因为驱动程序堆栈使用句柄来跟踪驱动程序可以使用支持的功能。

     例如，如果获取 USBD\_处理 (通过调用[ **USBD\_CreateHandle**](https://msdn.microsoft.com/library/windows/hardware/hh406241))，通过调用查询驱动程序堆栈[ **USBD\_QueryUsbCapability**](https://msdn.microsoft.com/library/windows/hardware/hh406230)，并通过调用分配 URB [ **USBD\_UrbAllocate**](https://msdn.microsoft.com/library/windows/hardware/hh406250)。 传递相同 USBD\_中这两个这些调用的句柄。

     如果您调用 KMDF 方法[ **WdfUsbTargetDeviceQueryUsbCapability** ](https://msdn.microsoft.com/library/windows/hardware/hh439434)并[ **WdfUsbTargetDeviceCreateUrb**](https://msdn.microsoft.com/library/windows/hardware/hh439423)，指定相同WDFUSBDEVICE 的句柄的方法调用中的框架目标对象。

   - 分配给 GUID 的 GUID\_USB\_功能\_静态\_流。
   - 输出缓冲区 （USHORT 指向）。 完成后在缓冲区充满 （每个终结点） 受主控制器的流的最大数目。
   - 输出缓冲区长度 （字节）。 对于流的长度是`sizeof (USHORT)`。

2. 返回的 NTSTATUS 值的计算结果。 如果成功完成例程，将返回状态\_成功时，静态流支持功能。 否则，该方法返回相应的错误代码。
3. 确定打开的流数。 可以打开的流的最大数目的限制：
   -   最大主机控制器支持的流数。 由接收数[ **WdfUsbTargetDeviceQueryUsbCapability** ](https://msdn.microsoft.com/library/windows/hardware/hh439434) (用于 WDM 驱动程序[ **USBD\_QueryUsbCapability** ](https://msdn.microsoft.com/library/windows/hardware/hh406230))，在调用方提供输出缓冲区中。 Microsoft 提供的 USB 驱动程序堆栈支持最多 255 个流。 **WdfUsbTargetDeviceQueryUsbCapability**采用这一限制到这一点时计算的流数。 该方法永不返回为大于 255 的值。
   -   支持的设备中的终结点的流的数目上限。 若要获取该数字，请检查终结点配套描述符 (请参阅[ **USB\_SUPERSPEED\_终结点\_配套\_描述符**](https://msdn.microsoft.com/library/windows/hardware/hh406269)中Usbspec.h)。 若要获取的终结点配套描述符，必须分析配置描述符。 若要获取配置描述符，客户端驱动程序必须调用[ **WdfUsbTargetDeviceRetrieveConfigDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff550098)方法。 必须使用帮助器例程[ **USBD\_ParseConfigurationDescriptorEx** ](https://msdn.microsoft.com/library/windows/hardware/ff539102)并[ **USBD\_ParseDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff539109). 有关代码示例中，请参阅示例函数名为中的 RetrieveStreamInfoFromEndpointDesc[如何枚举 USB 管道](how-to-get-usb-pipe-handles.md)。

   若要确定流的最大数目，请选择较小的主控制器和终结点支持的两个值。
4. 分配的数组[ **USBD\_流\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh406247)结构与*n*元素，其中*n*是若要打开的流的数量。 客户端驱动程序会释放此数组，该驱动程序完成后使用流。
5. 通过调用为打开流请求分配 URB [ **WdfUsbTargetDeviceCreateUrb** ](https://msdn.microsoft.com/library/windows/hardware/hh439423)方法。 如果调用成功完成，方法检索 WDF 内存对象和的地址[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923) USB 驱动程序堆栈分配的结构。

   <strong>WDM 驱动程序: * * 调用[ </strong>USBD\_UrbAllocate * *](<https://msdn.microsoft.com/library/windows/hardware/hh406250>)例程。

6. 设置用于打开流请求 URB 的格式。 使用 URB [  **\_URB\_打开\_静态\_流**](https://msdn.microsoft.com/library/windows/hardware/hh406294)结构定义的请求。 若要设置格式 URB 需要：
   -   终结点 USBD 管道句柄。 如果有 WDF 管道对象，则可以通过调用获取 USBD 管道句柄[ **WdfUsbTargetPipeWdmGetPipeHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff551162)方法。
   -   （在步骤 4 中创建） 的流数组
   -   一个指向[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)结构 （在步骤 5 中创建）。

   若要设置格式 URB，调用[ **UsbBuildOpenStaticStreamsRequest** ](https://msdn.microsoft.com/library/windows/hardware/hh406226)和参数值的形式传递所需的信息。 请确保为指定的流数**UsbBuildOpenStaticStreamsRequest**不超过支持的流的最大数目。
7. 通过调用作为 WDF 请求对象发送 URB [ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)方法。 若要以同步方式发送请求，调用[ **WdfUsbTargetDeviceSendUrbSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff550105)方法相反。

   * * WDM 驱动程序: * * 将 URB IRP，与相关联并将其提交到 USB 驱动程序堆栈 IRP。 有关详细信息，请参阅[如何提交 URB](send-requests-to-the-usb-driver-stack.md)。

8. 该请求是完成后，检查请求的状态。

   如果 USB 驱动程序堆栈使请求失败，URB 状态包含相关的错误代码。 一些常见的失败条件所述的备注部分。

如果请求 （IRP 或 WDF 请求对象） 的状态指示 USBD\_状态\_成功后，该请求已成功完成。 检查的数组[ **USBD\_流\_信息**](https://msdn.microsoft.com/library/windows/hardware/hh406247)完成时接收到的结构。 有关请求的流的信息填充的数组。 USB 驱动程序堆栈将填充与流的信息，如句柄数组中每个结构 (收到作为 USBD\_管道\_处理)，流标识符和传输大小的最大数目。 流现在已打开，以将数据传输。

打开流请求，将需要分配 URB 和数组。 客户端驱动程序必须通过调用释放 URB [ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)关联 WDF 内存对象上，打开的流请求完成后的方法。 如果该驱动程序发送请求以同步方式通过调用[ **WdfUsbTargetDeviceSendUrbSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff550105)，然后在方法返回之后，它必须释放 WDF 内存对象。 如果客户端驱动程序发送请求以异步方式调用[ **WdfRequestSend**](https://msdn.microsoft.com/library/windows/hardware/ff550027)，驱动程序必须释放与关联的驱动程序实现完成例程中的 WDF 内存对象请求。

客户端驱动程序是使用流已完成或已将其存储的 I/O 请求后，可以释放流数组。 在本主题中包含的代码示例，该驱动程序存储中的设备上下文的流数组。 驱动程序已释放的设备对象之前释放设备上下文。

### <a name="how-to-transfer-data-to-a-particular-stream"></a>如何将数据传输到的特定流

若要将数据传输请求发送到特定的流，将需要 WDF 请求对象。 通常情况下，客户端驱动程序不需要分配 WDF 请求对象。 当 I/O 管理器收到请求时从应用程序时，I/O 管理器创建请求 IRP。 该 IRP 截获由框架中。 然后，框架会分配 WDF 请求对象来表示 IRP。 然后，框架将 WDF 请求对象传递给客户端驱动程序。 然后，客户端驱动程序可以数据传输 URB 相关联的请求对象，并将其发送到 USB 驱动程序堆栈。

如果客户端驱动程序不会从框架接收 WDF 请求对象，并且想要以异步方式发送请求，该驱动程序必须通过调用分配 WDF request 对象[ **WdfRequestCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff549951)方法。 设置新对象的格式通过调用[ **WdfUsbTargetPipeFormatRequestForUrb**](https://msdn.microsoft.com/library/windows/hardware/ff551139)，并将发送通过调用请求[ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027).

在同步情况下，传递 WDF 请求对象是可选的。

若要将数据传输到流，必须使用 URBs。 必须通过调用格式化 URB [ **WdfUsbTargetPipeFormatRequestForUrb**](https://msdn.microsoft.com/library/windows/hardware/ff551139)。

下面的 WDF 方法是*不*支持流：

-   [**WdfUsbTargetPipeFormatRequestForRead**](https://msdn.microsoft.com/library/windows/hardware/ff551136)
-   [**WdfUsbTargetPipeFormatRequestForWrite**](https://msdn.microsoft.com/library/windows/hardware/ff551141)
-   [**WdfUsbTargetPipeReadSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551155)
-   [**WdfUsbTargetPipeWriteSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551163)

以下过程假设客户端驱动程序从框架接收的请求对象。

1.  通过调用分配 URB [ **WdfUsbTargetDeviceCreateUrb**](https://msdn.microsoft.com/library/windows/hardware/hh439423)。 此方法会分配一个包含新分配的 URB WDF 内存对象。 客户端驱动程序可以选择为每个 I/O 请求分配 URB 或分配 URB 和重复使用该相同类型的请求。
2.  通过调用来大容量复制格式化 URB [ **UsbBuildInterruptOrBulkTransferRequest**](https://msdn.microsoft.com/library/windows/hardware/ff538953)。 在中*PipeHandle*参数，指定到流的句柄。 在上一个请求中中, 所述获取流句柄[如何打开静态流](#open-streams)部分。
3.  通过调用格式化 WDF request 对象[ **WdfUsbTargetPipeFormatRequestForUrb** ](https://msdn.microsoft.com/library/windows/hardware/ff551139)方法。 在调用中，指定包含数据传输 URB WDF 内存对象。 在步骤 1 中分配的内存对象。
4.  发送 WDF 请求，或者通过调用 URB [ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)或[ **WdfUsbTargetPipeSendUrbSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551158)。 如果您调用**WdfRequestSend**，必须通过调用指定完成例程[ **WdfRequestSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff550030) ，以便可以获取客户端驱动程序时收到通知异步操作已完成。 必须释放数据传输 URB 中完成例程。

<strong>WDM 驱动程序: * * 通过调用分配 URB [ </strong>USBD\_UrbAllocate<strong> ](<https://msdn.microsoft.com/library/windows/hardware/hh406250>)并设置其格式为大容量传输 (请参阅[ </strong> \_URB\_大容量\_或者\_中断\_传输<strong>](<https://msdn.microsoft.com/library/windows/hardware/ff540352>))。若要设置格式 URB，可以调用[ </strong>UsbBuildInterruptOrBulkTransferRequest<strong> ](<https://msdn.microsoft.com/library/windows/hardware/ff538953>)或者手动格式化 URB 结构。指定流的句柄中 URB **UrbBulkOrInterruptTransfer.PipeHandle</strong>成员。

### <a name="how-to-close-static-streams"></a>如何关闭流，静态

该驱动程序完成后，客户端驱动程序可以关闭流，使用它们。 但是，关闭流请求是可选的。 USB 驱动程序堆栈取消配置与流关联的终结点时关闭所有的流。 终结点取消配置选择了备用配置或接口时，设备中删除，等等。 如果该驱动程序想要打开不同数量的流，客户端驱动程序必须关闭流。 若要发送关闭流请求：

1.  分配[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)结构通过调用[ **WdfUsbTargetDeviceCreateUrb**](https://msdn.microsoft.com/library/windows/hardware/hh439423)。
2.  设置为关闭流请求 URB 的格式。 **UrbPipeRequest**的成员[ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)结构[  **\_URB\_管道\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff540419)结构。 按如下所示填写其成员：
    -   **Hdr**的成员[  **\_URB\_管道\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff540419)必须 URB\_函数\_关闭\_静态\_流
    -   **PipeHandle**成员必须为包含打开的流中使用的终结点的句柄。

3.  发送 WDF 请求，或者通过调用 URB [ **WdfRequestSend** ](https://msdn.microsoft.com/library/windows/hardware/ff550027)或[ **WdfUsbTargetDeviceSendUrbSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff550105)。

关闭句柄请求关闭所有之前已通过客户端驱动程序打开的流。 客户端驱动程序不能使用请求关闭终结点中的特定流。

<a name="remarks"></a>备注
-------

**用于发送静态流请求的最佳实践**

USB 驱动程序堆栈上接收到 URB 执行验证的次数。 若要避免验证错误，客户端驱动程序必须考虑以下方面：

-   不到不支持流的终结点发送一个流打开或关闭流请求。 调用[ **WdfUsbTargetDeviceQueryUsbCapability** ](https://msdn.microsoft.com/library/windows/hardware/hh439434) (用于 WDM 驱动程序[ **USBD\_QueryUsbCapability**](https://msdn.microsoft.com/library/windows/hardware/hh406230)) 到确定静态流支持，并且仅发送流请求，如果终结点支持它们。
-   不要请求数量超过了流支持的最大数目 （的打开的流） 或发送请求，而无需指定的流数。 确定基于 USB 驱动程序堆栈和设备的终结点支持的流的数量的流的数量。
-   不到已打开的流的终结点发送的打开流请求。
-   不向不具有打开的流的终结点发送关闭流请求。
-   通过选择配置或选择接口请求获取静态流打开一个终结点的、 不发送 I/O 请求使用终结点管道处理后。 即使静态流已关闭，这是如此。

**重置和中止管道操作**

有时，传输到或从终结点可能会失败。 此类故障可以产生的错误条件的终结点或主机控制器上，例如停止或暂停条件。 若要清除的错误条件，客户端驱动程序首先取消仍在进行传输，然后重置终结点与之关联的管道。 若要取消仍在进行传输，客户端驱动程序可以发送的中止管道请求。 若要重置一个管道，客户端驱动程序必须发送重置管道请求。

在流传输的情况下中止管道和重置管道请求不支持与大容量终结点关联的各个流。 如果传输失败的特定流管道上，主控制器上所有其他管道 （适用于其他流） 停止传输。 若要从此错误条件，客户端驱动程序应手动取消传输到每个流。 然后，客户端驱动程序必须使用大容量终结点的管道句柄发送重置管道请求。 客户端驱动程序必须为该请求指定的管道句柄中的终结点[  **\_URB\_管道\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff540419)结构并设置 URB 函数 (**Hdr.Function**) 到 URB\_函数\_同步\_重置\_管道\_AND\_清除\_停滞。

## <a name="complete-example"></a>完整示例


下面的代码示例显示如何打开流。

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
[USB I/O 操作](usb-device-i-o.md)  



