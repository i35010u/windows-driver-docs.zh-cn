---
Description: An app that communicates with a USB device usually sends several control transfers requests.
title: 如何发送 USB 控制传输 （UWP 应用）
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b2251863942c5ab21c4fae499603422459930ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522388"
---
# <a name="how-to-send-a-usb-control-transfer-uwp-app"></a>如何发送 USB 控制传输 （UWP 应用）


**摘要**

-   如何设置 USB 安装数据包的格式
-   如何启动您的应用程序中的 USB 控制复制

**重要的 Api**

-   [**SendControlInTransferAsync**](https://msdn.microsoft.com/library/windows/apps/dn264027)
-   [**SendControlOutTransferAsync**](https://msdn.microsoft.com/library/windows/apps/dn264044)

通常与 USB 设备进行通信的应用将请求发送多个控制传输。 这些请求获取有关设备的信息并发送由硬件供应商定义的控制命令。 本主题中介绍有关控制传输以及如何设置格式并将其发送在 UWP 应用中。

控制传输可以读取或写入的配置信息或执行由硬件供应商定义的特定于设备的功能。 如果在传输中执行写入操作，则扩展传输;读取的操作，它是在传输。 无论方向如何，软件，例如 UWP 应用，在主机系统上始终生成并发出一个请求控制传输。 有时，您的应用程序可以启动控制传输的读取或写入数据。 在这种情况下，您可能需要将发送的附加缓冲区。

若要容纳所有类型的控制转移[ **Windows.Devices.Usb** ](https://msdn.microsoft.com/library/windows/apps/dn278466)提供这些方法：

-   [**SendControlOutTransferAsync (UsbSetupPacket)**](https://msdn.microsoft.com/library/windows/apps/dn264047)
-   [**SendControlInTransferAsync (UsbSetupPacket)**](https://msdn.microsoft.com/library/windows/apps/dn264037)
-   [**SendControlOutTransferAsync (UsbSetupPacket, IBuffer)**](https://msdn.microsoft.com/library/windows/apps/dn264050)
-   [**SendControlInTransferAsync (UsbSetupPacket, IBuffer)**](https://msdn.microsoft.com/library/windows/apps/dn264028)

![usb 控制传输适用于 windows 运行时 api，可用于 usb](images/scenario2-flowchart.png)

获取描述符的数据或发送标准命令还用于 USB 控制传输。 但是，我们建议通过调用由提供的特定方法发送这些类型的请求[ **Windows.Devices.Usb** ](https://msdn.microsoft.com/library/windows/apps/dn278466)而不是手动生成控制传输。 例如，若要选择一项备用设置，请调用[ **SelectSettingAsync** ](https://msdn.microsoft.com/library/windows/apps/dn264286)而不是调用[ **SendControlOutTransferAsync (UsbSetupPacket)**](https://msdn.microsoft.com/library/windows/apps/dn264047).

控制对于某些类型的标准请求不支持的传输。 但是，你的设备是否属于支持的设备类[ **Windows.Devices.Usb**](https://msdn.microsoft.com/library/windows/apps/dn278466)，可以发送一些请求，如设备类规范所定义。

## <a name="before-you-start"></a>开始之前...


-   则必须打开设备并获得[ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)对象。 读取[如何连接到 USB 设备 （UWP 应用）](how-to-connect-to-a-usb-device--uwp-app-.md)。
-   获取有关供应商定义的控制命令的信息。 这些命令通常是硬件规范中定义的。
-   可以看到在 CustomUsbDeviceAccess 示例中，Scenario2 本主题中所示的完整代码\_ControlTransfer.cpp 和 Scenario2\_ControlTransfer.h。

## <a name="step-1-populate-the-setup-packet"></a>第 1 步：填充安装数据包


在本主题中，我们将发送控制传输到设备中各种模式的灯将闪烁。 要填充的安装程序数据包，必须知道由硬件供应商定义的控制命令：

-   **bmRequestType** (D7):扩展
-   **bmRequestType** (D4):设备
-   **bmRequestType** (D6...D5):供应商
-   **bRequest**:0x03
-   **wValue**:0 到 7 （任何数字在该范围内，非独占）
-   **wIndex**:0
-   **并将 wLength**:0

控制传输时，您必须填充*安装程序数据包*包含有关传输的所有信息; 是否请求读取或写入数据、 请求类型等。 官方的 USB 规范中定义的安装程序数据包格式。 安装程序数据包字段的值由设备的硬件规范提供。

1.  创建[ **UsbSetupPacket** ](https://msdn.microsoft.com/library/windows/apps/dn278431)对象。
2.  填充[ **UsbSetupPacket** ](https://msdn.microsoft.com/library/windows/apps/dn278431)通过设置各种属性的对象。 此表显示了 USB 定义安装程序数据包字段，以及对应于这些字段的属性：

    | 中部分 9.3 的字段     | 属性                                                                              | 描述                                                                                                                                                                                                                            |
    |---------------------------|---------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | **bmRequestType** (D7)    | [**UsbControlRequestType.Direction**](https://msdn.microsoft.com/library/windows/apps/dn263833)      | 请求的方向。 请求是从主机到 (Out 传输） 的设备或设备主机到主机 （位于传输）。                                                                                                                 |
    | **bmRequestType** (D4)    | [**UsbControlRequestType.Recipient**](https://msdn.microsoft.com/library/windows/apps/dn263841)      | 请求的接收方。 所有控制传输都目标的默认终结点。 但是，接收方可能是设备、 接口、 终结点，或其他。 有关详细信息 USB 设备接口，终结点的层次结构，请参阅设备布局。 |
    | **bmRequestType** (D6...D5) | [**UsbControlRequestType.ControlTransferType**](https://msdn.microsoft.com/library/windows/apps/dn263829) | 请求的类别。 标准、 类或供应商。                                                                                                                                                                                       |
    | **bRequest**              | [**UsbSetupPacket.Request**](https://msdn.microsoft.com/library/windows/apps/dn278437)                        | 请求类型。 该请求是否是标准的请求，如 GET\_描述符请求，该请求 USB 规范所定义。 否则，它无法供应商定义。                                                           |
    | **wValue**                | [**UsbSetupPacket.Value**](https://msdn.microsoft.com/library/windows/apps/dn278452)                            | 取决于请求的类型。                                                                                                                                                                                                        |
    | **wIndex**                | [**UsbSetupPacket.Index**](https://msdn.microsoft.com/library/windows/apps/dn278433)                            | 取决于请求的类型。                                                                                                                                                                                                        |
    | **wLength**               | [**UsbSetupPacket.Length**](https://msdn.microsoft.com/library/windows/apps/dn278435)                          | 数据包的长度发送或接收该请求中。                                                                                                                                                                            |
**请注意**对于某些控制传输模式，您可能需要提供**bmRequestType**作为原始字节。 在这种情况下，您可以在设置字节[ **UsbControlRequestType.AsByte** ](https://msdn.microsoft.com/library/windows/apps/dn263827)属性。

## <a name="step-2-start-an-asynchronous-operation-to-send-the-control-transfer"></a>步骤 2：启动异步操作以发送的控制转移


若要发送的控制转移，必须具有[ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)对象。 控制传输可能会也可能不需要按照安装程序数据包的数据包。

若要启动控制传输，调用的重写[ **SendControlInTransferAsync** ](https://msdn.microsoft.com/library/windows/apps/dn264028)或[ **SendControlOutTransferAsync**](https://msdn.microsoft.com/library/windows/apps/dn264050)。 如果传输使用的数据包，然后调用**SendControlOutTransferAsync （UsbSetupPacket，IBuffer）**， **SendControlInTransferAsync （UsbSetupPacket，IBuffer）**。 这些方法采用一个附加参数，它包含要写入的数据或从设备接收数据。 使用流程图来确定该重写调用。

调用启动和异步操作。 操作完成后，该调用将返回[ **IAsyncOperation** ](https://msdn.microsoft.com/library/windows/desktop/br205802)对象，其中包含操作的结果。 对于扩展传输，该对象返回在传输中发送的字节数。 在传输，该对象包含包含已从设备读取的数据的缓冲区。

## <a name="usb-control-transfer-code-example"></a>USB 控制传输的代码示例


此示例代码演示如何发送更改 SuperMUTT 设备上的闪烁模式控制传输。 安装程序数据包传输包含供应商定义命令。 该示例处于 Scenario2\_ControlTransfer.cpp。

```ManagedCPlusPlus
async Task SetSuperMuttLedBlinkPatternAsync(Byte pattern)
        {
            UsbSetupPacket initSetupPacket = new UsbSetupPacket
            {
                RequestType = new UsbControlRequestType
                {
                    Direction = UsbTransferDirection.Out,
                    Recipient = UsbControlRecipient.Device,
                    ControlTransferType = UsbControlTransferType.Vendor
                },
                Request = SuperMutt.VendorCommand.SetLedBlinkPattern,
                Value = pattern,
                Length = 0
            };

            UInt32 bytesTransferred = await EventHandlerForDevice.Current.Device.SendControlOutTransferAsync(initSetupPacket);

            MainPage.Current.NotifyUser("The Led blink pattern is set to " + pattern.ToString(), NotifyType.StatusMessage);
        }
```

此示例代码演示如何发送更改 SuperMUTT 设备上的闪烁模式控制传输。 安装程序数据包传输包含供应商定义命令。 该示例处于 Scenario2\_ControlTransfer.cpp。

```CSharp
async Task<IBuffer> SendVendorControlTransferInToDeviceRecipientAsync(Byte vendorCommand, UInt32 dataPacketLength)
 {
    // Data will be written to this buffer when we receive it
    var buffer = new Windows.Storage.Streams.Buffer(dataPacketLength);

    UsbSetupPacket initSetupPacket = new UsbSetupPacket
    {
        RequestType = new UsbControlRequestType
        {
            Direction = UsbTransferDirection.In,
            Recipient = UsbControlRecipient.Device,
            ControlTransferType = UsbControlTransferType.Vendor,
        },
        Request = vendorCommand,
        Length = dataPacketLength
    };

    return await EventHandlerForDevice.Current.Device.SendControlInTransferAsync(initSetupPacket, buffer);
}
```








