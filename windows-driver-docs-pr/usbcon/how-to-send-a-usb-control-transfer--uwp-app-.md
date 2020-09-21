---
description: 与 USB 设备通信的应用通常会发送多个控制传输请求。
title: 如何发送 USB 控制传输（UWP 应用）
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58a285bf68f4a2af48df4521d77925e2b67c336a
ms.sourcegitcommit: 366a15d68eb58d01a8ca6de7b982f62ac8b7deaf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90811916"
---
# <a name="how-to-send-a-usb-control-transfer-uwp-app"></a>如何发送 USB 控制传输（UWP 应用）


**摘要**

-   如何格式化 USB 安装包
-   如何从应用启动 USB 控件传输

**重要的 API**

-   [**SendControlInTransferAsync**](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlInTransferAsync_Windows_Devices_Usb_UsbSetupPacket_Windows_Storage_Streams_IBuffer_)
-   [**SendControlOutTransferAsync**](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlOutTransferAsync_Windows_Devices_Usb_UsbSetupPacket_)

与 USB 设备通信的应用通常会发送多个控制传输请求。 这些请求将获取硬件供应商定义的设备和发送控制命令的相关信息。 在本主题中，你将了解如何进行控件传输，以及如何在 UWP 应用中设置其格式并发送它们。

控件传输可以读取或写入配置信息或执行由硬件供应商定义的特定于设备的功能。 如果传输执行了写入操作，则为传出传输;读取操作是传输。 不管方向如何，主机系统上的软件（例如 UWP 应用）始终会生成并启动控件传输请求。 有时，应用程序可以启动读取或写入数据的控制传输。 在这种情况下，可能需要发送额外的缓冲区。

为了适应各种类型的控制传输， [**Windows**](/uwp/api/Windows.Devices.Usb) azure 提供了以下方法：

-   [**SendControlOutTransferAsync (UsbSetupPacket) **](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlOutTransferAsync_Windows_Devices_Usb_UsbSetupPacket_)
-   [**SendControlInTransferAsync (UsbSetupPacket) **](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlInTransferAsync_Windows_Devices_Usb_UsbSetupPacket_)
-   [**SendControlOutTransferAsync (UsbSetupPacket，IBuffer) **](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlOutTransferAsync_Windows_Devices_Usb_UsbSetupPacket_Windows_Storage_Streams_IBuffer_)
-   [**SendControlInTransferAsync (UsbSetupPacket，IBuffer) **](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlInTransferAsync_Windows_Devices_Usb_UsbSetupPacket_Windows_Storage_Streams_IBuffer_)

![适用于 usb 的 windows 运行时 api 的 usb 控件传输](images/scenario2-flowchart.png)

USB 控制传输还用于获取描述符数据或发送标准命令。 但是，我们建议通过调用由 [**Windows**](/uwp/api/Windows.Devices.Usb) 提供的特定方法（而不是手动生成控件传输）来发送这些类型的请求。 例如，若要选择替代设置，请调用 [**SelectSettingAsync**](/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_SelectSettingAsync) 而不是调用 [**SendControlOutTransferAsync (UsbSetupPacket) **](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlOutTransferAsync_Windows_Devices_Usb_UsbSetupPacket_)。

不支持对某些类型的标准请求进行控制传输。 但是，如果你的设备属于 [**Windows**](/uwp/api/Windows.Devices.Usb)所支持的设备类，则可以发送一些请求，如设备类规范所定义。

## <a name="before-you-start"></a>开始之前...


-   必须打开设备并获得 [**UsbDevice**](/uwp/api/Windows.Devices.Usb.UsbDevice) 对象。 阅读 [如何)  (UWP 应用连接到 USB 设备 ](how-to-connect-to-a-usb-device--uwp-app-.md)。
-   获取有关供应商定义的控制命令的信息。 通常在硬件规范中定义这些命令。
-   你可以在 CustomUsbDeviceAccess 示例，Scenario2 \_ ControlTransfer 和 Scenario2 ControlTransfer 中查看本主题中所示的完整代码 \_ 。

## <a name="step-1-populate-the-setup-packet"></a>步骤1：填充安装包


在本主题中，我们会将控制传输发送到设备，该设备在各种模式下都呈灯光闪烁。 为了填充安装包，您必须知道由硬件供应商定义的控制命令：

-   **bmRequestType** (D7) ： OUT
-   **bmRequestType** (D4) ：设备
-   **bmRequestType** (D6 .。。D5) ：供应商
-   **bRequest**：0x03
-   **wValue**： 0-7 (该范围中的任何数字（包括) 
-   **wIndex**：0
-   **wLength**：0

对于控件传输，必须填充 *安装包* ，其中包含有关传输的所有信息;请求是读取还是写入数据、请求类型，等等。 安装包的格式是在官方 USB 规范中定义的。 安装包字段的值由设备的硬件规范提供。

1.  创建 [**UsbSetupPacket**](/uwp/api/Windows.Devices.Usb.UsbSetupPacket) 对象。
2.  通过设置各种属性填充 [**UsbSetupPacket**](/uwp/api/Windows.Devices.Usb.UsbSetupPacket) 对象。 此表显示了 USB 定义的安装包字段，以及对应于这些字段的属性：

| 第9.3 节中的字段 | Property | 说明 | 
|----------------|-----------------|-------------------------| 
| **bmRequestType** (D7)  | [**UsbControlRequestType**](/uwp/api/Windows.Devices.Usb.UsbControlRequestType#Windows_Devices_Usb_UsbControlRequestType_Direction) | 请求的方向。 无论请求是从主机到设备， (传出将) 或设备传输到 (传输) 中的主机。 |
| **bmRequestType** (D4)  | [**UsbControlRequestType**](/uwp/api/Windows.Devices.Usb.UsbControlRequestType#Windows_Devices_Usb_UsbControlRequestType_Recipient) | 请求的接收方。 所有控制传输均以默认终结点为目标。 但是，收件人可能是设备、接口、终结点或其他。 有关 USB 设备、接口、终结点层次结构的详细信息，请参阅设备布局。 |
| **bmRequestType** (D6 .。。D5)  | [**UsbControlRequestType.ControlTransferType**](/uwp/api/Windows.Devices.Usb.UsbControlRequestType#Windows_Devices_Usb_UsbControlRequestType_ControlTransferType) | 请求的类别。 标准、类或供应商。 |
| **bRequest** | [**UsbSetupPacket 请求**](/uwp/api/Windows.Devices.Usb.UsbSetupPacket#Windows_Devices_Usb_UsbSetupPacket_Request) | 请求类型。 如果请求是标准请求，如 GET \_ 描述符请求，则该请求由 USB 规范定义。 否则，它可以由供应商定义。 |
| **wValue** | [**UsbSetupPacket**](/uwp/api/Windows.Devices.Usb.UsbSetupPacket#Windows_Devices_Usb_UsbSetupPacket_Value) | 取决于请求的类型。 |
| **wIndex** | [**UsbSetupPacket**](/uwp/api/Windows.Devices.Usb.UsbSetupPacket#Windows_Devices_Usb_UsbSetupPacket_Index) | 取决于请求的类型。 |
| **wLength** | [**UsbSetupPacket**](/uwp/api/Windows.Devices.Usb.UsbSetupPacket#Windows_Devices_Usb_UsbSetupPacket_Length) |此请求中发送或接收的数据包的长度。|

**注意**  对于某些控件传输，可能需要提供 **bmRequestType** 作为原始字节。 在这种情况下，可以在 [**UsbControlRequestType. AsByte**](/uwp/api/Windows.Devices.Usb.UsbControlRequestType#Windows_Devices_Usb_UsbControlRequestType_AsByte) 属性中设置字节。

## <a name="step-2-start-an-asynchronous-operation-to-send-the-control-transfer"></a>步骤2：启动异步操作以发送控件传输


若要发送控制传输，必须有一个 [**UsbDevice**](/uwp/api/Windows.Devices.Usb.UsbDevice) 对象。 你的控件传输可能需要也可能不需要遵循安装包的数据包。

若要启动控件传输，请调用 [**SendControlInTransferAsync**](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlInTransferAsync_Windows_Devices_Usb_UsbSetupPacket_Windows_Storage_Streams_IBuffer_) 或 [**SendControlOutTransferAsync**](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlOutTransferAsync_Windows_Devices_Usb_UsbSetupPacket_Windows_Storage_Streams_IBuffer_)的重写。 如果传输使用数据包，请调用 **SendControlOutTransferAsync (UsbSetupPacket，IBuffer) **， **SendControlInTransferAsync (UsbSetupPacket，IBuffer) **。 这些方法采用其他参数，其中包含用于写入或接收设备数据的数据。 使用流程图确定要调用的替代。

调用开始和异步操作。 操作完成后，调用将返回包含操作结果的 [**iasyncoperation<tresult>**](/previous-versions/br205802(v=vs.85)) 对象。 对于 OUT 传输，对象返回传输中发送的字节数。 对于 IN 传输，对象包含包含从设备读取的数据的缓冲区。

## <a name="usb-control-transfer-code-example"></a>USB 控件传输代码示例


此代码示例演示如何发送更改 SuperMUTT 设备上闪烁模式的控制传输。 用于传输的安装包包含供应商定义的命令。 该示例位于 Scenario2 \_ ControlTransfer 中。

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

此代码示例演示如何发送更改 SuperMUTT 设备上闪烁模式的控制传输。 用于传输的安装包包含供应商定义的命令。 该示例位于 Scenario2 \_ ControlTransfer 中。

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