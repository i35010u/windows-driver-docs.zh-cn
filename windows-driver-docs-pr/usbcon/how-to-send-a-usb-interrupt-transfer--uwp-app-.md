---
description: USB 设备可以支持中断终结点，以便它可以定期发送或接收数据。
title: 如何发送 USB 中断传输请求（UWP 应用）
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f2827ff3f81ddd235a3a66a7acff761211b6ce2
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101730"
---
# <a name="how-to-send-a-usb-interrupt-transfer-request-uwp-app"></a>如何发送 USB 中断传输请求（UWP 应用）


**摘要**

-   当主机轮询设备时发生中断传输
-   实现 UsbInterruptInPipe 的事件处理程序[ **。 DataReceived**](/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe#Windows_Devices_Usb_UsbInterruptInPipe_DataReceived)
-   注册和注销事件处理程序

**重要的 API**

-   [**UsbInterruptInPipe**](/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe)
-   [**UsbInterruptOutPipe**](/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe)
-   [**UsbInterruptInEventArgs**](/uwp/api/Windows.Devices.Usb.UsbInterruptInEventArgs)

USB 设备可以支持中断终结点，以便它可以定期发送或接收数据。 为实现此目的，主机会定期轮询设备，并在每次主机轮询设备时传输数据。 中断传输主要用于从设备获取中断数据。 本主题介绍 UWP 应用如何从设备获取连续中断数据。

**中断终结点信息**

对于中断终结点，描述符公开了这些属性。 这些值仅用于信息，不应影响管理缓冲区传输缓冲区的方式。

-   数据的传输频率如何？

    通过获取端点描述符的 **间隔** 值获取该信息 (参阅 [**UsbInterruptOutEndpointDescriptor**](/uwp/api/Windows.Devices.Usb.UsbInterruptOutEndpointDescriptor#Windows_Devices_Usb_UsbInterruptOutEndpointDescriptor_Interval) 或 [**UsbInterruptInEndpointDescriptor**](/uwp/api/Windows.Devices.Usb.UsbInterruptInEndpointDescriptor#Windows_Devices_Usb_UsbInterruptInEndpointDescriptor_Interval)) 。 该值指示在总线上的每个帧中的设备上发送或接收数据的频率。

    **注意** **Interval** 属性不是在 USB 规范)  (定义的 **bInterval** 值。

    该值表示数据传输到设备或从设备传输的频率。 例如，对于高速设备，如果 **Interval** 为125微秒，则每125微秒传输一次数据。 如果 **Interval** 为1000微秒，则数据每毫秒传输一次。

-   可在每个服务间隔内传输多少数据？

    获取终结点描述符支持的最大数据包大小，以获取可传输的字节数 (参阅 UsbInterruptOutEndpointDescriptor. MaxPacketSize 或 MaxPacketSize。 设备速度限制的最大数据包大小。 对于低速设备，最多可达8个字节。 对于全速设备，最多64个字节。 对于高速高带宽设备，应用可以发送或接收超过最大数据包大小（每个 microframe 最多3072字节）。

    **注意**  SuperSpeed 设备上的中断终结点能够传输更多的字节。 此值由 USB **wBytesPerInterval** \_ SUPERSPEED \_ 终结点 \_ 伴随 \_ 描述符的 wBytesPerInterval 指示。 若要检索描述符，请使用 [**UsbEndpointDescriptor**](/uwp/api/Windows.Devices.Usb.UsbControlRequestType#Windows_Devices_Usb_UsbControlRequestType_AsByte) 属性获取描述符缓冲区，然后使用 [**DataReader**](/uwp/api/Windows.Storage.Streams.DataReader) 方法分析该缓冲区。



**中断传出传输**

USB 设备可以支持按固定间隔从主机接收数据的中断终结点。 当主机每次轮询设备时，主机就会发送数据。 UWP 应用可以启动中断传输请求，指定要发送的数据。 当设备确认主机中的数据时，该请求即已完成。 UWP 应用可以将数据写入 [**UsbInterruptOutPipe**](/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe)。

**传输中断**

相反，USB 设备可以支持终结点中断，作为通知主机设备生成的硬件中断的方式。 通常，USB 人体学接口设备 (HID) 例如键盘和指针设备支持中断输出终结点。 发生中断时，终结点会存储中断数据，但数据不会立即到达主机。 终结点必须等待主机控制器对设备进行轮询。 由于在生成时间和到达主机之间必须存在最小延迟，因此它会定期轮询设备。 UWP 应用可在 [**UsbInterruptInPipe**](/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe)中获取收到的数据。 当主机收到设备数据时完成的请求。

## <a name="before-you-start"></a>开始之前...


-   必须已打开设备并获得 [**UsbDevice**](/uwp/api/Windows.Devices.Usb.UsbDevice) 对象。 阅读 [如何)  (UWP 应用连接到 USB 设备 ](how-to-connect-to-a-usb-device--uwp-app-.md)。
-   在 CustomUsbDeviceAccess 示例，Scenario3 InterruptPipes 文件中，可以看到本主题中所示的完整代码 \_ 。

## <a name="writing-to-the-interrupt-out-endpoint"></a>写入中断结束终结点


应用发送中断传输请求的方式与大容量传输完全相同，不同之处在于目标是一个中断管道，由 [**UsbInterruptOutPipe**](/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe)表示。 有关详细信息，请参阅 [如何将 USB 批量传输请求发送 (UWP 应用) ](how-to-send-a-usb-bulk-transfer--uwp-app-.md)。

## <a name="step-1-implement-the-interrupt-event-handler-interrupt-in"></a>步骤1：在) 中实现中断事件处理程序 (中断


当将数据从设备接收到中断管道时，它会引发 [**DataReceived**](/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe#Windows_Devices_Usb_UsbInterruptInPipe_DataReceived) 事件。 若要获取中断数据，应用程序必须实现事件处理程序。 处理程序的 *eventArgs* 参数指向数据缓冲区。

此代码示例显示了事件处理程序的简单实现。 处理程序维护收到的中断的计数。 每次调用处理程序时，它都会递增计数。 处理程序从 *eventArgs* 参数获取数据缓冲区，并显示中断数和接收的字节数。

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

## <a name="step-2-get-the-interrupt-pipe-object-interrupt-in"></a>步骤2：在) 中 (中断获取中断管道对象


若要为 [**DataReceived**](/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe#Windows_Devices_Usb_UsbInterruptInPipe_DataReceived) 事件注册事件处理程序，请使用以下任何属性获取对 [**UsbInterruptInPipe**](/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe) 的引用：

-   如果你的中断终结点在第一个 USB 接口中存在，则为[**UsbDevice DefaultInterface。 \[ \] **](/uwp/api/Windows.Devices.Usb.UsbInterface)
-   [**UsbDevice.Configu。UsbInterfaces \[ m \] 。InterruptInPipes \[ n \] **](/uwp/api/Windows.Devices.Usb.UsbInterface)用于枚举设备支持的每个接口的管道中的所有中断。
-   [**UsbInterface. InterfaceSettings \[ m \] 。InterruptInEndpoints \[ n \] 。**](/uwp/api/Windows.Devices.Usb.UsbInterface) 用于枚举接口的设置定义的管道中的中断的管道。
-   用于从终结点中中断的终结点描述符获取管道对象的[**UsbEndpointDescriptor. AsInterruptInEndpointDescriptor。**](/uwp/api/Windows.Devices.Usb.UsbInterruptInEndpointDescriptor#Windows_Devices_Usb_UsbInterruptInEndpointDescriptor_Pipe)

**注意**  避免通过枚举当前未选择的接口设置的中断终结点来获取管道对象。 若要传输数据，管道必须与活动设置中的终结点相关联。



## <a name="step-3-register-the-event-handler-to-start-receiving-data-interrupt-in"></a>步骤3：注册事件处理程序以开始在) 接收数据 (中断


接下来，必须在引发[**DataReceived**](/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe#Windows_Devices_Usb_UsbInterruptInPipe_DataReceived)事件的[**UsbInterruptInPipe**](/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe)对象上注册事件处理程序。

此代码示例演示如何注册事件处理程序。 在此示例中，类跟踪事件处理程序、为其注册事件处理程序的管道，以及管道当前是否正在接收数据。 所有这些信息用于取消注册事件处理程序，如下面的步骤所示。

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

注册事件处理程序后，每次在关联的中断管道中接收数据时，都会调用此处理程序。

## <a name="step-4-unregister-the-event-handler-to-stop-receiving-data-interrupt-in"></a>步骤4：取消注册事件处理程序，以停止在) 中接收数据 (中断


完成数据接收后，取消注册事件处理程序。

此代码示例演示如何取消注册事件处理程序。 在此示例中，如果应用程序具有以前注册的事件处理程序，则该方法将获取跟踪的事件处理程序，并在中断管道上将其注销。

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

取消注册事件处理程序后，应用程序将停止从中断管道接收数据，因为在中断事件上不会调用事件处理程序。 这并不意味着中断管道会停止获取数据。