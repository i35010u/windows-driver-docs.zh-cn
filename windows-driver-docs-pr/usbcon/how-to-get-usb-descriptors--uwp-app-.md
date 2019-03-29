---
Description: 一个与 USB 设备进行交互的主要任务是获取有关它的信息。
title: 如何获取 USB 描述符（UWP 应用）
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d18df5103cc11a300748a3070e212b015dd38b79
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349974"
---
# <a name="how-to-get-usb-descriptors-uwp-app"></a>如何获取 USB 描述符（UWP 应用）


**摘要**

-   了解 USB 设备布局
-   获取标准 USB 描述符
-   获取自定义描述符

**重要的 Api**

-   [**UsbDeviceDescriptor**](https://msdn.microsoft.com/library/windows/apps/dn263961)
-   [**UsbConfigurationDescriptor**](https://msdn.microsoft.com/library/windows/apps/dn297689)
-   [**UsbDescriptor**](https://msdn.microsoft.com/library/windows/apps/dn263863)

一个与 USB 设备进行交互的主要任务是获取有关它的信息。 所有 USB 设备都提供的多个数据结构称为描述符窗体中的信息。 本主题介绍如何为 UWP 应用可以从终结点、 接口、 配置和设备级别的设备获取描述符。

## <a name="usb-descriptors"></a>USB 描述符


USB 设备描述了其功能在两个主要的描述符： 设备描述符和配置描述符。

USB 设备必须提供*设备描述符*，包含有关 USB 设备作为一个整体的信息。 如果设备不提供该描述符，或提供的格式不正确的描述符，Windows 将无法加载设备驱动程序。 描述符中的最重要信息是设备的*硬件 ID*设备 (组合**供应商 ID**并**产品 ID**字段)。 它基于 Windows 能够匹配设备的现成驱动程序的信息。 另一个是键的信息是*最大数据包大小*的默认终结点 (**MaxPacketSize0**)。 默认终结点是所有的目标请求，主机将发送到设备对其进行配置。

设备描述符的长度被固定。

USB 设备还必须提供一个完整*配置描述符*。 此描述符的开头部分已修复的 9 个字节的长度，其余部分是可变长度具体取决于大量接口和终结点支持这些接口。 固定长度部分提供了有关 USB 配置的信息： 数目的接口支持和功率消耗时在设备处于该配置。 这些初始的 9 个字节后跟的可变部分提供有关所有 USB 接口信息的描述符。 每个设置组成一组终结点和每个接口包含一个或多个接口设置。 描述符的接口、 替代设置和终结点包含在变量部分。

有关设备布局的详细说明，请参阅[标准 USB 描述符](standard-usb-descriptors.md)。

## <a name="before-you-start"></a>开始之前...


-   您必须打开设备并获取[ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)对象。 读取[如何连接到 USB 设备 （UWP 应用）](how-to-connect-to-a-usb-device--uwp-app-.md)。
-   可以看到在 CustomUsbDeviceAccess 示例中，Scenario5 本主题中所示的完整代码\_UsbDescriptors 文件。
-   获取有关设备布局的信息。 **Usbview.exe** （包括针对 Windows 8 的 Windows 软件开发工具包 (SDK) 中） 是使您能够浏览所有 USB 控制器和连接到它们的 USB 设备的应用程序。 对于每个连接的设备，可以查看设备、 配置、 接口和终结点描述符，以了解有关设备的功能。

## <a name="how-to-get-the-device-descriptor"></a>如何获取设备描述符


UWP 应用可以从以前获取获取设备描述符[ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)对象通过获取[ **UsbDevice.DeviceDescriptor** ](https://msdn.microsoft.com/library/windows/apps/dn264002)属性值。

此代码示例演示如何填充从设备描述符字段值的字符串。

```CSharp
String GetDeviceDescriptorAsString (UsbDevice device)
{
    String content = null;

    var deviceDescriptor = device.DeviceDescriptor;

    content = "Device Descriptor\n"
            + "\nUsb Spec Number : 0x" + deviceDescriptor.BcdUsb.ToString("X4", NumberFormatInfo.InvariantInfo)
            + "\nMax Packet Size (Endpoint 0) : " + deviceDescriptor.MaxPacketSize0.ToString("D", NumberFormatInfo.InvariantInfo)
            + "\nVendor ID : 0x" + deviceDescriptor.IdVendor.ToString("X4", NumberFormatInfo.InvariantInfo)
            + "\nProduct ID : 0x" + deviceDescriptor.IdProduct.ToString("X4", NumberFormatInfo.InvariantInfo)
            + "\nDevice Revision : 0x" + deviceDescriptor.BcdDeviceRevision.ToString("X4", NumberFormatInfo.InvariantInfo)
            + "\nNumber of Configurations : " + deviceDescriptor.NumberOfConfigurations.ToString("D", NumberFormatInfo.InvariantInfo);
    
    return content;
}
```

输出如下所示：

![usb 设备描述符](images/device-descriptors-app.png)

## <a name="how-to-get-the-configuration-descriptor"></a>如何获取配置描述符


若要配置描述符的固定的部分获得以前获得[ **UsbDevice** ](https://msdn.microsoft.com/library/windows/apps/dn263883)对象，

1.  获取[ **UsbConfiguration** ](https://msdn.microsoft.com/library/windows/apps/dn297681)对象[ **UsbDevice**](https://msdn.microsoft.com/library/windows/apps/dn263883)。 **UsbConfiguration**表示设备定义的第一个 USB 配置和基础设备驱动程序还选择默认情况下。
2.  获取[ **UsbConfiguration.ConfigurationDescriptor** ](https://msdn.microsoft.com/library/windows/apps/dn263799)属性值。

配置描述符的固定的部分指示设备的 power 特征。 例如，确定设备是否从总线或外部源消耗电源 (请参阅[ **UsbConfigurationDescriptor.SelfPowered**](https://msdn.microsoft.com/library/windows/apps/dn263787))。 如果设备总线消耗电源，（以 milliamp 为单位） 多少能源消耗 (请参阅[ **UsbConfigurationDescriptor.MaxPowerMilliamps**](https://msdn.microsoft.com/library/windows/apps/dn297702))。 此外，确定设备是否能够通过获取唤醒本身或从低功耗状态，系统[ **UsbConfigurationDescriptor.RemoteWakeup** ](https://msdn.microsoft.com/library/windows/apps/dn263785)值。

此代码示例演示如何在字符串中获取配置描述符的固定的部分。

```CSharp
String GetConfigurationDescriptorAsString(UsbDevice device)
{
    String content = null;

    var usbConfiguration = device.Configuration;
    var configurationDescriptor = usbConfiguration.ConfigurationDescriptor;

    content = "Configuration Descriptor\n"
            + "\nNumber of Interfaces : " + usbConfiguration.UsbInterfaces.Count.ToString("D", NumberFormatInfo.InvariantInfo)
            + "\nConfiguration Value : 0x" + configurationDescriptor.ConfigurationValue.ToString("X2", NumberFormatInfo.InvariantInfo)
            + "\nSelf Powered : " + configurationDescriptor.SelfPowered.ToString()
            + "\nRemote Wakeup : " + configurationDescriptor.RemoteWakeup.ToString()
            + "\nMax Power (milliAmps) : " + configurationDescriptor.MaxPowerMilliamps.ToString("D", NumberFormatInfo.InvariantInfo);

    return content;
}
```

输出如下所示：

![usb 配置描述符](images/config-desc-app.png)

## <a name="how-to-get-interface-descriptors"></a>如何获取接口描述符


接下来，可以获取有关 USB 接口的一部分配置的信息。

USB 接口是界面设置的集合。 这种情况下没有任何描述符来描述整个接口。 术语*接口描述符*指示描述了界面中的设置的数据结构。

[ **Windows.Devices.Usb** ](https://msdn.microsoft.com/library/windows/apps/dn278466)命名空间公开了可用于获取有关每个 USB 接口的信息的对象和所有接口 （适用于替代设置） 该接口中包含的描述符。 和描述符从配置描述符的长度可变的部分。

若要获取从接口描述符[ **UsbConfiguration**](https://msdn.microsoft.com/library/windows/apps/dn297681)，

1.  通过获取获取配置中的接口的数组[ **UsbConfiguration.UsbInterfaces** ](https://msdn.microsoft.com/library/windows/apps/dn263808)属性。
2.  为每个接口 ([**UsbInterface**](https://msdn.microsoft.com/library/windows/apps/dn264121))，获取此信息：
    -   大容量和中断管道的处于活动状态并可将数据传输。
    -   在界面中的替代设置的数组。
    -   接口描述符的数组。

此代码示例获取所有[ **UsbInterface** ](https://msdn.microsoft.com/library/windows/apps/dn264121)配置对象。 每个对象，从帮助器方法获取替代设置和打开的大容量和界面管道的数。 如果设备支持多个接口，设备类、 子类和协议的每个接口的代码可能有所不同。 但是，替代设置的所有接口描述符必须都指定相同的代码。 在此示例中，该方法可获取设备类、 子类和协议代码的第一个设置，以确定整个界面的代码的接口描述符中。

```CSharp
String GetInterfaceDescriptorsAsString(UsbDevice device)
{
    String content = null;
    
    var interfaces = device.Configuration.UsbInterfaces;

    content = "Interface Descriptors";

        foreach (UsbInterface usbInterface in interfaces)
        {
            // Class/subclass/protocol values from the first interface setting.

            UsbInterfaceDescriptor usbInterfaceDescriptor = usbInterface.InterfaceSettings[0].InterfaceDescriptor;

            content +="\n\nInterface Number: 0x" +usbInterface.InterfaceNumber.ToString("X2", NumberFormatInfo.InvariantInfo)
                    + "\nClass Code: 0x" +usbInterfaceDescriptor.ClassCode.ToString("X2", NumberFormatInfo.InvariantInfo)
                    + "\nSubclass Code: 0x" +usbInterfaceDescriptor.SubclassCode.ToString("X2", NumberFormatInfo.InvariantInfo)
                    + "\nProtocol Code: 0x" +usbInterfaceDescriptor.ProtocolCode.ToString("X2", NumberFormatInfo.InvariantInfo)
                    + "\nNumber of Interface Settings: "+usbInterface.InterfaceSettings.Count.ToString("D", NumberFormatInfo.InvariantInfo)
                    + "\nNumber of open Bulk In pipes: "+usbInterface.BulkInPipes.Count.ToString("D", NumberFormatInfo.InvariantInfo)
                    + "\nNumber of open Bulk Out pipes: "+usbInterface.BulkOutPipes.Count.ToString("D", NumberFormatInfo.InvariantInfo)
                    + "\nNumber of open Interrupt In pipes: "+usbInterface.InterruptInPipes.Count.ToString("D", NumberFormatInfo.InvariantInfo)
                    + "\nNumber of open Interrupt Out pipes: "+usbInterface.InterruptOutPipes.Count.ToString("D", NumberFormatInfo.InvariantInfo);
       }

    return content;
}
```

输出如下所示：

![usb 接口描述符](images/interface-desc-app.png)

## <a name="how-to-get-endpoint-descriptors"></a>如何获取终结点描述符


（除默认控制终结点） 的所有 USB 终结点必须都具有终结点描述符。 若要获取特定终结点的终结点描述符，您必须知道该接口并替代终结点属于的设置。

1.  获取[ **UsbInterface** ](https://msdn.microsoft.com/library/windows/apps/dn264121)包含终结点的对象。
2.  通过获取获取替代设置的数组[ **UsbInterface.InterfaceSettings**](https://msdn.microsoft.com/library/windows/apps/dn264291)。
3.  该数组中找到的设置 ([**UsbInterfaceSetting**](https://msdn.microsoft.com/library/windows/apps/dn264278)) 使用终结点。
4.  在每个设置，通过枚举大容量和中断描述符数组中找到此终结点。

    由这些对象表示终结点描述符：

    -   [**UsbBulkInEndpointDescriptor**](https://msdn.microsoft.com/library/windows/apps/dn297543)
    -   [**UsbBulkOutEndpointDescriptor**](https://msdn.microsoft.com/library/windows/apps/dn297619)
    -   [**UsbInterruptInEndpointDescriptor**](https://msdn.microsoft.com/library/windows/apps/dn264294)
    -   [**UsbInterruptOutEndpointDescriptor**](https://msdn.microsoft.com/library/windows/apps/dn278420)

如果你的设备具有只有一个接口，则可以使用[ **UsbDevice.DefaultInterface** ](https://msdn.microsoft.com/library/windows/apps/dn263998)来获得接口，在此示例代码所示。 在这里，帮助器方法获取使用字符串填充 active 界面设置管道与相关联的终结点描述符。

```CSharp
private String GetEndpointDescriptorsAsString(UsbDevice device)
{
    String content = null;

    var usbInterface = device.DefaultInterface;
    var bulkInPipes = usbInterface.BulkInPipes;
    var bulkOutPipes = usbInterface.BulkOutPipes;
    var interruptInPipes = usbInterface.InterruptInPipes;
    var interruptOutPipes = usbInterface.InterruptOutPipes;

    content = "Endpoint Descriptors for open pipes";

    // Print Bulk In Endpoint descriptors
    foreach (UsbBulkInPipe bulkInPipe in bulkInPipes)
    {
        var endpointDescriptor = bulkInPipe.EndpointDescriptor;

        content +="\n\nBulk In Endpoint Descriptor"
                + "\nEndpoint Number : 0x" + endpointDescriptor.EndpointNumber.ToString("X2", NumberFormatInfo.InvariantInfo)
                + "\nMax Packet Size : " + endpointDescriptor.MaxPacketSize.ToString("D", NumberFormatInfo.InvariantInfo);
    }

    // Print Bulk Out Endpoint descriptors
    foreach (UsbBulkOutPipe bulkOutPipe in bulkOutPipes)
    {
        var endpointDescriptor = bulkOutPipe.EndpointDescriptor;

        content +="\n\nBulk Out Endpoint Descriptor"
                + "\nEndpoint Number : 0x" + endpointDescriptor.EndpointNumber.ToString("X2", NumberFormatInfo.InvariantInfo)
                + "\nMax Packet Size : " + endpointDescriptor.MaxPacketSize.ToString("D", NumberFormatInfo.InvariantInfo);
    }

    // Print Interrupt In Endpoint descriptors
    foreach (UsbInterruptInPipe interruptInPipe in interruptInPipes)
    {
        var endpointDescriptor = interruptInPipe.EndpointDescriptor;

        content +="\n\nInterrupt In Endpoint Descriptor"
                + "\nEndpoint Number : 0x" + endpointDescriptor.EndpointNumber.ToString("X2", NumberFormatInfo.InvariantInfo)
                + "\nMax Packet Size : " + endpointDescriptor.MaxPacketSize.ToString("D", NumberFormatInfo.InvariantInfo);
                + "\nInterval : " + endpointDescriptor.Interval.Duration.ToString();
    }

    // Print Interrupt Out Endpoint descriptors
    foreach (UsbInterruptOutPipe interruptOutPipe in interruptOutPipes)
    {
        var endpointDescriptor = interruptOutPipe.EndpointDescriptor;

        content +="\n\nInterrupt Out Endpoint Descriptor"
                + "\nEndpoint Number : 0x" + endpointDescriptor.EndpointNumber.ToString("X2", NumberFormatInfo.InvariantInfo)
                + "\nMax Packet Size : " + endpointDescriptor.MaxPacketSize.ToString("D", NumberFormatInfo.InvariantInfo);
                + "\nInterval : " + endpointDescriptor.Interval.Duration.ToString();
    }

    return content;
}
```

输出如下所示：

![usb 终结点描述符](images/endpoint-desc-app.png)

## <a name="how-to-get-custom-descriptors"></a>如何获取自定义说明符


请注意， [ **UsbConfiguration**](https://msdn.microsoft.com/library/windows/apps/dn297681)， [ **UsbInterface**](https://msdn.microsoft.com/library/windows/apps/dn264121)，并[ **UsbInterfaceSetting**](https://msdn.microsoft.com/library/windows/apps/dn264278)对象，每个公开名为的属性**描述符**。 属性值检索由表示描述符的数组[ **UsbDescriptor** ](https://msdn.microsoft.com/library/windows/apps/dn263863)对象。 **UsbDescriptor**对象允许应用在缓冲区中获取描述符的数据。 [**UsbDescriptor.DescriptorType** ](https://msdn.microsoft.com/library/windows/apps/dn263870)并[ **UsbDescriptor.Length** ](https://msdn.microsoft.com/library/windows/apps/dn263874)属性存储的类型和保存描述符所需的缓冲区的长度。

**请注意**  前两个字节的所有描述符缓冲区还指示的类型和长度的描述符。

 

例如， [ **UsbConfiguration.Descriptors** ](https://msdn.microsoft.com/library/windows/apps/dn264289)属性获取的完整配置描述符 （固定和可变长度的分区） 的数组。 该数组中的第一个元素是固定长度配置描述符 (与相同[ **UsbConfigurationDescriptor**](https://msdn.microsoft.com/library/windows/apps/dn297689))，第二个元素是第一个备用设置，接口描述符等等。

同样， [ **UsbInterface.Descriptors** ](https://msdn.microsoft.com/library/windows/apps/dn264289)属性获取的接口的所有描述符和相关终结点描述符的数组。 [ **UsbInterfaceSetting.Descriptors** ](https://msdn.microsoft.com/library/windows/apps/dn264281)属性获取的所有描述符的数组，该设置，例如终结点描述符。

获取描述符的这种方式时，应用程序需要检索自定义说明符或其他终结点配套描述符的 SuperSpeed 设备等描述符。

此代码示例演示如何在配置描述符从缓冲区获取描述符数据。 示例将获取配置描述符集并分析该集内包含的所有描述符。 每个描述符，它使用 DataReader 对象来读取缓冲区，并显示描述符长度和类型。 在此示例中所示，可以获取自定义描述符。

```CSharp
private String GetCustomDescriptorsAsString(UsbDevice device)
{
    String content = null;
    // Descriptor information will be appended to this string and then printed to UI
    content = "Raw Descriptors";

    var configuration = device.Configuration;
    var allRawDescriptors = configuration.Descriptors;

    // Print first 2 bytes of all descriptors within the configuration descriptor    
    // because the first 2 bytes are always length and descriptor type
    // the UsbDescriptor's DescriptorType and Length properties, but we will not use these properties
    // in order to demonstrate ReadDescriptorBuffer() and how to parse it.

    foreach (UsbDescriptor descriptor in allRawDescriptors)
    {
        var descriptorBuffer = new Windows.Storage.Streams.Buffer(descriptor.Length);
        descriptor.ReadDescriptorBuffer(descriptorBuffer);

        DataReader reader = DataReader.FromBuffer(descriptorBuffer);

        // USB data is Little Endian according to the USB spec.
        reader.ByteOrder = ByteOrder.LittleEndian;

        // ReadByte has a side effect where it consumes the current byte, so the next ReadByte will read the next character.
        // Putting multiple ReadByte() on the same line (same variable assignment) may cause the bytes to be read out of order.
        var length = reader.ReadByte().ToString("D", NumberFormatInfo.InvariantInfo);
        var type = "0x" + reader.ReadByte().ToString("X2", NumberFormatInfo.InvariantInfo);

        content += "\n\nDescriptor"
                + "\nLength : " + length
                + "\nDescriptorType : " + type;
    }

    return content;
}
```

 

 




