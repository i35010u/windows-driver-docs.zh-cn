---
Description: USB 设备可以支持中断终结点，以便它可以发送或接收的数据按固定间隔。
title: 如何发送 USB 中断传输请求（UWP 应用）
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4d294b7beb2e1be0ba8566faea72261b771a631
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378292"
---
# <a name="how-to-send-a-usb-interrupt-transfer-request-uwp-app"></a>如何发送 USB 中断传输请求（UWP 应用）


**摘要**

-   中断主机轮询设备时发生传输
-   实现的事件处理程序[ **UsbInterruptInPipe.DataReceived**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe#Windows_Devices_Usb_UsbInterruptInPipe_DataReceived)
-   注册和注销事件处理程序

**重要的 API**

-   [**UsbInterruptInPipe**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe)
-   [**UsbInterruptOutPipe**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe)
-   [**UsbInterruptInEventArgs**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInEventArgs)

USB 设备可以支持中断终结点，以便它可以发送或接收的数据按固定间隔。 若要完成此操作，主机轮询设备按固定间隔和传输主机轮询设备每次数据。 中断传送主要用于从设备获取中断数据。 本主题介绍如何为 UWP 应用可以从设备获取持续中断数据。

**中断终结点信息**

对于中断终结点，该描述符显示这些属性。 这些值仅供参考，不应影响如何管理缓冲区传输缓冲区。

-   何种频率传输数据？

    获取该信息通过获取**间隔**终结点描述符的值 (请参阅[ **UsbInterruptOutEndpointDescriptor.Interval** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutEndpointDescriptor#Windows_Devices_Usb_UsbInterruptOutEndpointDescriptor_Interval)或[ **UsbInterruptInEndpointDescriptor.Interval**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInEndpointDescriptor#Windows_Devices_Usb_UsbInterruptInEndpointDescriptor_Interval))。 值表示何种频率发送到或从总线上每个帧中的设备接收数据。

    **请注意** **间隔**属性不是**bInterval** （USB 规范中定义） 的值。

    值表示何种频率数据到或从设备传输。 例如，对于高速度设备，如果**间隔**125 微秒为单位，每 125 微秒为单位传输数据。 如果**间隔**为 1000年毫秒，则传输的数据每隔一毫秒。

-   可以在每个服务间隔传输多少数据？

    获取通过获取终结点说明符支持的最大数据包大小可以传输的字节数 （请参阅 UsbInterruptOutEndpointDescriptor.MaxPacketSize 或 UsbInterruptInEndpointDescriptor.MaxPacketSize。 最大数据包大小受限制的设备的速度。 对于较慢的设备最多 8 个字节。 对于全速设备，最多 64 字节。 对于高速、 高带宽的设备，应用程序发送或接收个以上的最大数据包大小最多每 microframe 3072 字节数。

    **请注意**中断 SuperSpeed 设备上的终结点都能够传输更多的字节数。 值将由**wBytesPerInterval**的 USB\_SUPERSPEED\_终结点\_配套\_描述符。 若要检索描述符，通过获取描述符缓冲区[ **UsbEndpointDescriptor.AsByte** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbControlRequestType#Windows_Devices_Usb_UsbControlRequestType_AsByte)属性，然后通过使用缓冲的分析[ **DataReader**](https://docs.microsoft.com/uwp/api/Windows.Storage.Streams.DataReader)方法。



**中断输出传输**

USB 设备可以支持按固定间隔从主机接收数据的中断扩展终结点。 主机轮询设备，每次主机发送数据。 UWP 应用可以启动带指定要发送的数据的传输请求中断。 该请求完成时在设备确认收到来自主机的数据。 UWP 应用可以将数据写入[ **UsbInterruptOutPipe**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe)。

**中断 IN 传输**

相反，USB 设备可以支持作为一种方法来通知主机有关由设备生成的硬件中断的中断在终结点。 通常 USB 人体学接口设备 (HID) 如键盘和指针设备支持终结点中断。 当发生中断时，该终结点将中断数据存储，但数据将不会立即访问主机。 终结点必须等待主机控制器来轮询设备。 由于必须有最小时间数据之间的延迟会生成并到达主机，它会定期轮询设备。 UWP 应用可以获取数据中收到[ **UsbInterruptInPipe**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe)。 当数据从设备接收主机时完成请求。

## <a name="before-you-start"></a>开始之前...


-   您必须打开设备并获取[ **UsbDevice** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice)对象。 读取[如何连接到 USB 设备 （UWP 应用）](how-to-connect-to-a-usb-device--uwp-app-.md)。
-   可以看到在 CustomUsbDeviceAccess 示例中，Scenario3 本主题中所示的完整代码\_InterruptPipes 文件。

## <a name="writing-to-the-interrupt-out-endpoint"></a>写入到输出终结点中断


该应用将发送出传输请求中断等同出传输，只是目标大容量的方法是管道，由表示出中断[ **UsbInterruptOutPipe**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe)。 有关详细信息，请参阅[如何将发送的 USB 大容量传输请求 （UWP 应用）](how-to-send-a-usb-bulk-transfer--uwp-app-.md)。

## <a name="step-1-implement-the-interrupt-event-handler-interrupt-in"></a>第 1 步：实现中断事件处理程序 (中断 IN)


当数据从设备接收到中断管道时，将引发[ **DataReceived** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe#Windows_Devices_Usb_UsbInterruptInPipe_DataReceived)事件。 若要获取中断数据，应用必须实现一个事件处理程序。 *EventArgs*参数处理程序，指向数据缓冲区。

此示例代码显示了事件处理程序的简单实现。 该处理程序维护中断接收到的计数。 每次调用该处理程序时，它增加计数。 在处理程序获得中的数据缓冲区*eventArgs*参数，并显示收到的中断计数和字节的长度。

```CSharp
private async void OnInterruptDataReceivedEvent(UsbInterruptInPipe sender, UsbInterruptInEventArgs eventArgs)
{
    numInterruptsReceived++;

    // The data from the interrupt
    IBuffer buffer = eventArgs.InterruptData;

    // Create a DispatchedHandler for the because we are interracting with the UI directly and the
    // thread that this function is running on may not be the UI thread; if a non-UI thread modifies
    // the UI, an exception is thrown

    await Dispatcher.RunAsync(
                       CoreDispatcherPriority.Normal,
                       new DispatchedHandler(() =>
    {
        ShowData(
        "Number of interrupt events received: " + numInterruptsReceived.ToString()
        + "\nReceived " + buffer.Length.ToString() + " bytes");
    }));
}
```

```ManagedCPlusPlus
void OnInterruptDataReceivedEvent(UsbInterruptInPipe^ /* sender */, UsbInterruptInEventArgs^  eventArgs )
{
    numInterruptsReceived++;

    // The data from the interrupt
    IBuffer^ buffer = eventArgs->InterruptData;

    // Create a DispatchedHandler for the because we are interracting with the UI directly and the
    // thread that this function is running on may not be the UI thread; if a non-UI thread modifies
    // the UI, an exception is thrown

    MainPage::Current->Dispatcher->RunAsync(
        CoreDispatcherPriority::Normal,
        ref new DispatchedHandler([this, buffer]()
        {
            ShowData(
                "Number of interrupt events received: " + numInterruptsReceived.ToString()
                + "\nReceived " + buffer->Length.ToString() + " bytes",
                NotifyType::StatusMessage);
        }));
}
```

## <a name="step-2-get-the-interrupt-pipe-object-interrupt-in"></a>步骤 2：获取中断管道对象 (中断 IN)


若要注册的事件处理程序[ **DataReceived** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe#Windows_Devices_Usb_UsbInterruptInPipe_DataReceived)事件时，获取对引用[ **UsbInterruptInPipe** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe)通过使用任何这些属性：

-   [**UsbDevice.DefaultInterface.InterruptInPipes\[n\]**  ](https://msdn.microsoft.com/library/windows/apps/dn264292)如果你中断的终结点位于第一个 USB 接口。
-   [**UsbDevice.Configuration.UsbInterfaces\[m\]。InterruptInPipes\[n\]**  ](https://msdn.microsoft.com/library/windows/apps/dn264292)用于枚举所有中断中每个接口，设备支持的管道。
-   [**UsbInterface.InterfaceSettings\[m\]。InterruptInEndpoints \[n\]。管道**](https://msdn.microsoft.com/library/windows/apps/dn264292)用于枚举中断在管道定义的接口的设置。
-   [**UsbEndpointDescriptor.AsInterruptInEndpointDescriptor.Pipe** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInEndpointDescriptor#Windows_Devices_Usb_UsbInterruptInEndpointDescriptor_Pipe)的中断 IN 终结点的终结点描述符，从中获取管道对象。

**请注意**避免获取管道对象的枚举的当前未选界面设置中断终结点。 若要将数据传输，管道必须与活动设置中的终结点相关联。



## <a name="step-3-register-the-event-handler-to-start-receiving-data-interrupt-in"></a>步骤 3:注册事件处理程序来开始接收数据 (中断 IN)


接下来，必须在注册事件处理程序[ **UsbInterruptInPipe** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe)引发对象[ **DataReceived** ](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe#Windows_Devices_Usb_UsbInterruptInPipe_DataReceived)事件。

此示例代码演示如何注册事件处理程序。 在此示例中，此类跟踪的事件处理程序，用于注册事件处理程序，并且是否管道当前正在接收数据管道。 所有这些信息用于取消注册事件处理程序下, 一步中所示。

```CSharp
private void RegisterForInterruptEvent(TypedEventHandler<UsbInterruptInPipe, UsbInterruptInEventArgs> eventHandler)
{
    // Search for the correct pipe that has the specified endpoint number
    interruptPipe = usbDevice.DefaultInterface.InterruptInPipes[0];

    // Save the interrupt handler so we can use it to unregister
    interruptEventHandler = eventHandler;

    interruptPipe.DataReceived += interruptEventHandler;

    registeredInterruptHandler = true;
}
```

```CSharp
void RegisterForInterruptEvent(TypedEventHandler<UsbInterruptInPipe, UsbInterruptInEventArgs> eventHandler)
    // Search for the correct pipe that has the specified endpoint number
    interruptInPipe = usbDevice.DefaultInterface.InterruptInPipes.GetAt(pipeIndex);

    // Save the token so we can unregister from the event later
    interruptEventHandler = interruptInPipe.DataReceived += eventHandler;

    registeredInterrupt = true;    

}
```

注册事件处理程序后，调用此操作每次收到数据时在关联的中断管道中。

## <a name="step-4-unregister-the-event-handler-to-stop-receiving-data-interrupt-in"></a>步骤 4：取消注册事件处理程序，若要停止接收数据 (中断 IN)


结束接收数据之后，取消注册事件处理程序。

此示例代码演示如何取消注册事件处理程序。 在此示例中，如果应用了一个以前注册的事件处理程序方法获取跟踪的事件处理程序，并在中断管道上注销。

```CSharp
private void UnregisterInterruptEventHandler()
{
    if (registeredInterruptHandler)
    {
        interruptPipe.DataReceived -= interruptEventHandler;

        registeredInterruptHandler = false;
    }
}
```

```CSharp
void UnregisterFromInterruptEvent(void)
{
    if (registeredInterrupt)
    {
        interruptInPipe.DataReceived -= eventHandler;

        registeredInterrupt = false;
    }
}
```

注销事件处理程序后，应用的停止从中断管道接收数据，因为事件处理程序不中断事件上调用。 这并不意味着中断管道停止获取数据。