---
description: 了解 USB 批量传输，以及如何从 UWP 应用启动传输请求，以与 USB 设备通信。
title: 如何将发送 USB 大容量传输请求（UWP 应用）
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d4dbb3fc1bad258f7a271174adfc81c64177da2
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010546"
---
# <a name="how-to-send-a-usb-bulk-transfer-request-uwp-app"></a>如何将发送 USB 大容量传输请求（UWP 应用）

在本主题中，你将了解有关 USB 批量传输的信息，以及如何从 UWP 应用启动与 USB 设备通信的传输请求。

USB 全速、高速和 SuperSpeed 设备可以支持大容量终结点。 这些终结点用于传输大量的数据，例如将数据传输到 USB 闪存驱动器或从 USB 闪存驱动器传输数据。 大容量传输是可靠的，因为它们允许错误检测并涉及有限的重试次数，以确保主机或设备接收数据。 大容量传输用于非时间关键数据。 仅当总线上没有未使用的带宽时，数据才会传输。 因此，当总线忙于其他传输时，大容量数据可以无限期等待。

大容量终结点是单向的，在一次传输中，数据可以按进出方向传输。 若要支持读取和写入大容量数据，设备必须支持大容量和大容量输出终结点。 Bulk IN endpoint 用于将数据从设备读入主机，并使用 bulk 终结点将数据从主机发送到设备。

若要启动批量传输请求，应用必须具有对表示终结点的 *管道* 的引用。 管道是设备驱动程序在配置设备时打开的通信通道。 对于应用程序，管道是终结点的逻辑表示形式。 若要从终结点读取数据，应用将从管道中的关联批量获取数据。 为了将数据写入到终结点，应用程序将数据发送到 bulk OUT 管道。 对于批量读取和写入管道，请使用 [**UsbBulkInPipe**](/uwp/api/Windows.Devices.Usb.UsbBulkInPipe) 和 [**UsbBulkOutPipe**](/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe) 类。

应用还可以通过设置某些策略标志来修改管道的行为。 例如，对于读取请求，可以设置一个标志，该标志自动清除管道上的隔栏条件。 有关这些标志的信息，请参阅 [**UsbReadOptions**](/uwp/api/Windows.Devices.Usb.UsbReadOptions) 和 [**UsbWriteOptions**](/uwp/api/Windows.Devices.Usb.UsbWriteOptions)。

## <a name="before-you-start"></a>准备工作

* 必须打开设备并获得 [**UsbDevice**](/uwp/api/Windows.Devices.Usb.UsbDevice) 对象。 阅读 [如何)  (UWP 应用连接到 USB 设备 ](how-to-connect-to-a-usb-device--uwp-app-.md)。
* 在 [CustomUsbDeviceAccess 示例](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CustomUsbDeviceAccess)，Scenario4 BulkPipes 文件中，可以看到本主题中所示的完整代码 \_ 。

## <a name="step-1-get-the-bulk-pipe-object"></a>步骤1：获取大容量管道对象

若要启动传输请求，必须获取对大容量管道对象的引用 ([**UsbBulkOutPipe**](/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe) 或 [**UsbBulkInPipe**](/uwp/api/Windows.Devices.Usb.UsbBulkInPipe)) 。 可以通过枚举所有接口的所有设置来获取管道。 但是，对于数据传输，只能使用活动设置的管道。 如果关联的终结点不在活动设置中，则为 null。

<table>
  <thead>
    <tr>
      <th>若希望...</th>
      <th>使用此属性值</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <tr>
      <td rowspan="5">向大容量管道发送数据，获取对 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe"><strong>UsbBulkOutPipe</strong></a>的引用。</td>
      </tr>
      <tr>
      <td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_BulkOutPipes"><strong>UsbDevice. DefaultInterface. BulkOutPipes [n]</strong></a> 如果设备配置公开了一个 USB 接口。</td>
      </tr>
      <tr>
      <td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_BulkOutPipes"><strong>UsbDevice.Configu。UsbInterfaces [m]。BulkOutPipes [n]</strong></a>) 用于枚举设备支持的多个接口中的批量输出管道。</td>
      </tr>
       <td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutEndpointDescriptor#Windows_Devices_Usb_UsbInterruptOutEndpointDescriptor_Pipe"><strong>UsbInterface. InterfaceSettings \[ m \] 。BulkOutEndpoints [n]。</strong></a> 用于枚举接口中设置所定义的批量输出管道的管道。</td>
      </tr>
      <tr>
      <td>用于从大容量终结点的终结点描述符获取管道对象的<a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutEndpointDescriptor#Windows_Devices_Usb_UsbInterruptOutEndpointDescriptor_Pipe"><strong>UsbEndpointDescriptor. AsBulkOutEndpointDescriptor。</strong></a>
      </td>
      </tr>
    </tr>
    <tr>
      <tr>
        <td rowspan="5">接收批量管道中的数据，你可以获取 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe"><strong>UsbBulkInPipe</strong></a> 对象</td>
      </tr>
       <tr>
        <td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_BulkInPipes"><strong>UsbDevice. DefaultInterface. BulkInPipes [n]</strong></a> 如果设备配置公开了一个 USB 接口。</td>
       </tr>
       <tr>
       <td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_BulkInPipes"><strong>UsbDevice.Configu。UsbInterfaces [m]。BulkInPipes [n]</strong></a> 用于枚举设备支持的多个接口中的管道。</td>
       </tr>
       <tr>
       <td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInEndpointDescriptor#Windows_Devices_Usb_UsbBulkInEndpointDescriptor_Pipe"><strong>UsbInterface. InterfaceSettings [m]。BulkInEndpoints [n]。</strong></a> 用于枚举由接口中的设置定义的管道的管道。</td>
       </tr>
       <tr>
        <td>用于从大容量的终结点的终结点描述符获取管道对象的<a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInEndpointDescriptor#Windows_Devices_Usb_UsbBulkInEndpointDescriptor_Pipe"><strong>UsbEndpointDescriptor AsBulkInEndpointDescriptor。</strong></a></td>
      </tr>
    </tr>
  </tbody>
</table>

请注意：应为活动设置，或者需要 null 检查。

## <a name="step-2-configure-the-bulk-pipe-optional"></a>步骤2：配置批量管道 (可选) 

您可以通过在检索到的批量管道上设置某些标志来修改读取或写入操作的行为。

若要从设备读取，请将 [**UsbBulkInPipe**](/uwp/api/Windows.Devices.Usb.UsbBulkInPipe#Windows_Devices_Usb_UsbBulkInPipe_ReadOptions) 属性设置为 [**UsbReadOptions**](/uwp/api/Windows.Devices.Usb.UsbReadOptions)中定义的值之一。 对于写入，请将 [**UsbBulkOutPipe**](/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe#Windows_Devices_Usb_UsbBulkOutPipe_WriteOptions) 属性设置为 **UsbWriteOptions**中定义的值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>若希望...</th>
<th>设置此标志</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>自动清除终结点上的任何错误条件，而不停止数据流</p></td>
<td><strong>AutoClearStall</strong>
<p>有关详细信息，请参阅 <a href="#clearing-stall-conditions">清除卡住状态</a>。 此标志适用于读取和写入传输。</p></td>
</tr>
<tr class="even">
<td><p>发送多个具有最高效率的读取请求。 通过跳过错误检查来提高性能。</p></td>
<td><strong>OverrideAutomaticBufferManagement</strong>
<p>数据请求可以分为一个或多个传输，其中每个传输包含一定数量的被称为 <em>最大传输大小</em>的字节数。 对于多个传输，由于驱动程序执行的错误检查，导致两次传输排队可能会延迟。 此标志将跳过该错误检查。 若要获取最大传输大小，请使用 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe#Windows_Devices_Usb_UsbBulkInPipe_MaxTransferSizeBytes" data-raw-source="[&lt;strong&gt;UsbBulkInPipe.MaxTransferSizeBytes&lt;/strong&gt;](/uwp/api/Windows.Devices.Usb.UsbBulkInPipe#Windows_Devices_Usb_UsbBulkInPipe_MaxTransferSizeBytes)"><strong>UsbBulkInPipe. MaxTransferSizeBytes</strong></a> 属性。 如果请求大小为 <strong>UsbBulkInPipe. MaxTransferSizeBytes</strong>，则必须设置此标志。 注意：</p>
<p></p>
<div class="alert">重要说明<br/><p>如果设置此标志，则必须在管道的最大数据包大小的倍数中请求数据。 该信息存储在终结点描述符中。 大小取决于设备的总线速度。 对于全速、高速和 SuperSpeed，最大数据包大小分别为64、512和1024字节。 若要获取该值，请使用 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInEndpointDescriptor#Windows_Devices_Usb_UsbBulkInEndpointDescriptor_MaxPacketSize" data-raw-source="[&lt;strong&gt;UsbBulkInPipe.EndpointDescriptor.MaxPacketSize&lt;/strong&gt;](/uwp/api/Windows.Devices.Usb.UsbBulkInEndpointDescriptor#Windows_Devices_Usb_UsbBulkInEndpointDescriptor_MaxPacketSize)"><strong>UsbBulkInPipe. EndpointDescriptor. MaxPacketSize</strong></a> 属性。</p>
</div>
<div>

</div>
此标志仅适用于读取传输。</td>
</tr>
<tr class="odd">
<td><p>使用长度为零的数据包终止写入请求</p></td>
<td><strong>ShortPacketTerminate</strong>
<p>发送一个长度为零的数据包，以指示传出传输结束。此标志仅适用于写入传输。</p></td>
</tr>
<tr class="even">
<td><p>禁用读取短数据包 (小于终结点支持的最大数据包大小) </p></td>
<td><strong>IgnoreShortPacket</strong>
<p>默认情况下，如果设备发送的字节数小于最大数据包大小，应用程序将接收它们。 如果不想接收短数据包，请设置此标志。</p>
<p>此标志仅适用于读取传输。</p></td>
</tr>
</tbody>
</table>

## <a name="step-3-set-up-the-data-stream"></a>步骤3：设置数据流

当设备发送大容量数据时，将在大容量管道的输入流中接收数据。 下面是获取输入流的步骤：

1. 通过获取 [**UsbBulkInPipe. InputStream**](/uwp/api/Windows.Devices.Usb.UsbBulkInPipe#Windows_Devices_Usb_UsbBulkInPipe_InputStream) 属性获取对输入流的引用。
2. 通过在[**DataReader 构造函数**](/uwp/api/Windows.Storage.Streams.DataReader#Windows_Storage_Streams_DataReader__ctor_Windows_Storage_Streams_IInputStream_)中指定输入流来创建[**datareader**](/uwp/api/Windows.Storage.Streams.DataReader)对象。

若要将数据写入设备，应用必须在大容量管道上写入输出流。 下面是准备输出流的步骤：

1. 通过获取 [**UsbBulkOutPipe. OutputStream**](/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe#Windows_Devices_Usb_UsbBulkOutPipe_OutputStream) 属性获取对输出流的引用。
2. 通过在[**DataWriter**](/uwp/api/Windows.Storage.Streams.DataWriter#Windows_Storage_Streams_DataWriter__ctor_Windows_Storage_Streams_IOutputStream_)构造函数中指定输出流来创建一个[**DataWriter**](/uwp/api/Windows.Storage.Streams.DataWriter)对象。
3. 填充与输出流关联的数据缓冲区。
4. 根据数据类型，可以通过调用 [**DataWriter 方法**](/uwp/api/Windows.Storage.Streams.DataWriter#Windows_Storage_Streams_DataWriter__ctor_Windows_Storage_Streams_IOutputStream_)（如 [**WriteBytes**](/uwp/api/Windows.Storage.Streams.DataWriter#Windows_Storage_Streams_DataWriter_WriteBytes_System_Byte___)）将传输数据写入输出流。

## <a name="step-4-start-an-asynchronous-transfer-operation"></a>步骤4：启动异步传输操作

批量传输是通过异步操作启动的。

若要读取大容量数据，请通过调用 [**LoadAsync**](/uwp/api/Windows.Storage.Streams.DataReader#Windows_Storage_Streams_DataReader_LoadAsync_System_UInt32_)启动异步读取操作。

若要编写大容量数据，请通过调用 [**DataWriter**](/uwp/api/Windows.Storage.Streams.DataWriter#Windows_Storage_Streams_DataWriter_StoreAsync)来启动异步写入操作。

## <a name="step-5-get-results-of-the-read-transfer-operation"></a>步骤5：获取读取传输操作的结果

异步数据操作完成后，可以从 task 对象中获取读取或写入的字节数。 对于读取操作，请调用 [**DataReader 方法**](/uwp/api/Windows.Storage.Streams.DataReader)（如 [**ReadBytes**](/uwp/api/Windows.Storage.Streams.DataReader#Windows_Storage_Streams_DataReader_ReadBytes_System_Byte___)），以从输入流读取数据。

## <a name="clearing-stall-conditions"></a>清除隔栏条件

有时，应用可能会遇到失败的数据传输。 故障转移可能是由于终结点上出现延迟的情况。 只要终结点停止，就不能写入或读取数据。 若要继续进行数据传输，应用程序必须清除关联管道上的延迟情况。

应用可以将管道配置为在发生时自动清除隔间状态。 为此，请将 ReadOptions 属性设置为**UsbReadOptions** ，将[**UsbBulkInPipe**](/uwp/api/Windows.Devices.Usb.UsbBulkInPipe#Windows_Devices_Usb_UsbBulkInPipe_ReadOptions) [**或 UsbBulkOutPipe**](/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe#Windows_Devices_Usb_UsbBulkOutPipe_WriteOptions)属性设置为**WriteOptions**。 通过这种自动配置，应用程序不会遇到失败的传输，数据传输体验是无缝的。

若要手动清除隔间的情况，请在管道中调用 [**ClearStallAsync 的 UsbBulkInPipe**](/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe#Windows_Devices_Usb_UsbInterruptInPipe_ClearStallAsync) ;为大容量 OUT 管道调用 [**ClearStallAsync UsbBulkOutPipe**](/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe#Windows_Devices_Usb_UsbBulkOutPipe_ClearStallAsync) 。

**注意**  隔栏条件不指示空的终结点。 如果终结点中没有数据，则传输完成，但 length 为零字节。

对于读取操作，你可能需要在启动新的传输请求之前清除管道中的挂起数据。 为此，请调用 [**UsbBulkInPipe. FlushBuffer**](/previous-versions/windows/hardware/network/ff551975(v=vs.85)) 方法。

## <a name="usb-bulk-transfer-code-example"></a>USB 批量传输代码示例

此代码示例演示如何写入到大容量管道。 该示例将数据发送到默认接口上的第一个 bulk OUT 管道。 它将管道配置为在传输结束时发送长度为零的数据包。 传输完成后，将显示字节数。

```CSharp
    private async void BulkWrite()
    {
        String dataBuffer = "Hello World!";
        UInt32 bytesWritten = 0;

        UsbBulkOutPipe writePipe = usbDevice.DefaultInterface.BulkOutPipes[0];
        writePipe.WriteOptions |= UsbWriteOptions.ShortPacketTerminate;

        var stream = writePipe.OutputStream;

        DataWriter writer = new DataWriter(stream);

        writer.WriteString(dataBuffer);

        try
        {
            bytesWritten = await writer.StoreAsync();
        }
        catch (Exception exception)
        {
            ShowStatus(exception.Message.ToString());
        }
        finally
        {
            ShowStatus("Data written: " + bytesWritten + " bytes.");
        }
    }
```

此代码示例演示如何从大容量管道中读取。 该示例从默认接口上的第一个批量传入管道中检索数据。 它将管道配置为获得最大效率，并以最大数据包大小的块接收数据。 传输完成后，将显示字节数。

```CSharp
    private async void BulkRead()
    {
        UInt32 bytesRead = 0;

        UsbBulkInPipe readPipe = usbDevice.DefaultInterface.BulkInPipes[0];
        readPipe.ReadOptions |= UsbReadOptions.IgnoreShortPacket;

        var stream = readPipe.InputStream;
        DataReader reader = new DataReader(stream);

        try
        {
            bytesRead = await reader.LoadAsync(readPipe.EndpointDescriptor.MaxPacketSize);
        }
        catch (Exception exception)
        {
            ShowStatus(exception.Message.ToString());
        }
        finally
        {
            ShowStatus("Number of bytes: " + bytesRead);

            IBuffer buffer = reader.ReadBuffer(bytesRead);

            ShowData (buffer.ToString());

        }
    }
```