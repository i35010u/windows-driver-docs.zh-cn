---
description: 与 USB 设备交互的主要任务之一就是获取相关信息。
title: 如何获取 USB 描述符（UWP 应用）
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cf9889f5fac381c93d8d5e87cb163d8d7584ab3
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010635"
---
# <a name="how-to-get-usb-descriptors-uwp-app"></a>如何获取 USB 描述符（UWP 应用）


**摘要**

-   了解 USB 设备布局
-   获取标准 USB 描述符
-   获取自定义描述符

**重要的 API**

-   [**UsbDeviceDescriptor**](/uwp/api/Windows.Devices.Usb.UsbDeviceDescriptor)
-   [**UsbConfigurationDescriptor**](/uwp/api/Windows.Devices.Usb.UsbConfigurationDescriptor)
-   [**UsbDescriptor**](/uwp/api/Windows.Devices.Usb.UsbDescriptor)

与 USB 设备交互的主要任务之一就是获取相关信息。 所有 USB 设备都以几个称为描述符的数据结构形式提供信息。 本主题介绍 UWP 应用如何从设备上的终结点、接口、配置和设备级别获取描述符。

## <a name="usb-descriptors"></a>USB 描述符


USB 设备在两个主要描述符中描述了其功能：设备描述符和配置描述符。

USB 设备必须提供一个 *设备描述符* ，其中包含作为一个整体的 USB 设备的信息。 如果设备不提供该描述符或提供格式不正确的描述符，则 Windows 无法加载设备驱动程序。 描述符中最重要的信息是设备的 *硬件 ID* (**供应商 ID** 和 **产品 ID** 字段) 的组合。 这取决于 Windows 能够匹配设备的内置驱动程序的信息。 另一个是密钥的信息是默认终结点的 *最大数据包大小* (**MaxPacketSize0**) 。 默认终结点是主机发送到设备以对其进行配置的所有控制请求的目标。

设备描述符的长度是固定的。

USB 设备还必须提供完整的 *配置描述符*。 此描述符的开始部分的固定长度为9个字节，rest 是可变长度的，具体取决于这些接口支持的接口和终结点的数量。 固定长度部分提供有关 USB 配置的信息：设备支持的接口数量，以及设备处于该配置时的功率消耗。 这些初始9个字节后面是描述符的可变部分，它提供了有关所有 USB 接口的信息。 每个接口都由一个或多个接口设置组成，每个设置由一组终结点组成。 变量部分包含了接口、替代设置和终结点的说明符。

有关设备布局的详细说明，请参阅 [标准 USB 描述符](standard-usb-descriptors.md)。

## <a name="before-you-start"></a>开始之前...


-   必须已打开设备并获得 [**UsbDevice**](/uwp/api/Windows.Devices.Usb.UsbDevice) 对象。 阅读 [如何)  (UWP 应用连接到 USB 设备 ](how-to-connect-to-a-usb-device--uwp-app-.md)。
-   在 CustomUsbDeviceAccess 示例，Scenario5 UsbDescriptors 文件中，可以看到本主题中所示的完整代码 \_ 。
-   获取有关设备布局的信息。 适用于 windows) 8 的 Windows 软件开发工具包 (SDK) 中包含**Usbview.exe** (，它是一个应用程序，它使你能够浏览所有 USB 控制器和连接到它们的 usb 设备。 对于每个连接的设备，你可以查看设备、配置、接口和终结点描述符，以了解有关设备功能的信息。

## <a name="how-to-get-the-device-descriptor"></a>如何获取设备描述符


UWP 应用可通过获取[**UsbDevice DeviceDescriptor**](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DeviceDescriptor)属性值从以前获取的[**UsbDevice**](/uwp/api/Windows.Devices.Usb.UsbDevice)对象获取设备描述符。

此代码示例演示如何使用设备描述符中的字段值填充字符串。

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


若要从以前获取的 [**UsbDevice**](/uwp/api/Windows.Devices.Usb.UsbDevice) 对象获取配置描述符的固定部分，

1.  从[**UsbDevice**](/uwp/api/Windows.Devices.Usb.UsbDevice)获取[**UsbConfiguration**](/uwp/api/Windows.Devices.Usb.UsbConfiguration)对象。 **UsbConfiguration** 表示设备定义的第一个 USB 配置，并且在默认情况下由基础设备驱动程序选择。
2.  获取 [**UsbConfiguration.ConfigurationDescriptor**](/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_ConfigurationDescriptor) 属性值。

配置描述符的固定部分指示设备的电源特征。 例如，你可以确定设备是否从总线或外部源中消耗电源 (请参阅 [**SelfPowered**](/uwp/api/Windows.Devices.Usb.UsbConfigurationDescriptor#Windows_Devices_Usb_UsbConfigurationDescriptor_SelfPowered)) 。 如果设备消耗的是总线的电源，milliamp 单元中的电量 ()  (参阅 [**MaxPowerMilliamps**](/uwp/api/Windows.Devices.Usb.UsbConfigurationDescriptor#Windows_Devices_Usb_UsbConfigurationDescriptor_MaxPowerMilliamps)) 。 此外，还可以通过获取 [**RemoteWakeup**](/uwp/api/Windows.Devices.Usb.UsbConfigurationDescriptor#Windows_Devices_Usb_UsbConfigurationDescriptor_RemoteWakeup) 值，确定设备是否能够从低功率状态唤醒或系统。

此代码示例演示如何获取字符串中配置描述符的固定部分。

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


接下来，你可以获取有关作为配置的一部分的 USB 接口的信息。

USB 接口是接口设置的集合。 因此，没有描述整个接口的说明符。 术语 *接口描述符* 指示用于描述接口中的设置的数据结构。

[**Windows. u**](/uwp/api/Windows.Devices.Usb)命名空间公开的对象可用于获取有关每个 Usb 接口的信息以及该接口中包含的备用设置)  (的所有接口描述符。 和来自配置描述符的可变长度部分的说明符。

若要从 [**UsbConfiguration**](/uwp/api/Windows.Devices.Usb.UsbConfiguration)获取接口描述符，

1.  获取 [**UsbConfiguration UsbInterfaces**](/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_UsbInterfaces) 属性，获取配置中的接口数组。
2.  对于每个接口 ([**UsbInterface**](/uwp/api/Windows.Devices.Usb.UsbInterface)) ，请获取以下信息：
    -   处于活动状态并可以传输数据的批量和中断管道。
    -   接口中的替代设置的数组。
    -   接口描述符的数组。

此代码示例获取配置的所有 [**UsbInterface**](/uwp/api/Windows.Devices.Usb.UsbInterface) 对象。 在每个对象中，帮助器方法获取替代设置的数目，并打开大容量和接口管道。 如果设备支持多个接口，则每个接口的设备类、子类和协议代码可能会有所不同。 但是，替代设置的所有接口描述符必须指定相同的代码。 在此示例中，方法从第一个设置的接口描述符中获取设备类、子类和协议代码，以确定整个接口的代码。

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


除了默认控制终结点) 之外，所有 USB 终结点都必须具有终结点描述符 (。 若要获取特定终结点的终结点描述符，必须知道终结点属于哪个接口和备用设置。

1.  获取包含终结点的 [**UsbInterface**](/uwp/api/Windows.Devices.Usb.UsbInterface) 对象。
2.  通过获取 [**InterfaceSettings**](/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_InterfaceSettings)获取备用设置的数组。
3.  在数组中，查找使用终结点 ([**UsbInterfaceSetting**](/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting)) 的设置。
4.  在每个设置中，通过枚举大容量和中断描述符数组查找终结点。

    终结点描述符由以下对象表示：

    -   [**UsbBulkInEndpointDescriptor**](/uwp/api/Windows.Devices.Usb.UsbBulkInEndpointDescriptor)
    -   [**UsbBulkOutEndpointDescriptor**](/uwp/api/Windows.Devices.Usb.UsbBulkOutEndpointDescriptor)
    -   [**UsbInterruptInEndpointDescriptor**](/uwp/api/Windows.Devices.Usb.UsbInterruptInEndpointDescriptor)
    -   [**UsbInterruptOutEndpointDescriptor**](/uwp/api/Windows.Devices.Usb.UsbInterruptOutEndpointDescriptor)

如果设备只有一个接口，则可以使用 [**UsbDevice**](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DefaultInterface) 来获取接口，如下面的示例代码所示。 此处，helper 方法获取使用与活动接口设置的管道关联的终结点描述符来填充字符串。

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

## <a name="how-to-get-custom-descriptors"></a>如何获取自定义描述符


请注意， [**UsbConfiguration**](/uwp/api/Windows.Devices.Usb.UsbConfiguration)、 [**UsbInterface**](/uwp/api/Windows.Devices.Usb.UsbInterface)和 [**UsbInterfaceSetting**](/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting) 对象每个都公开一个名为 **描述符**的属性。 该属性值检索由 [**UsbDescriptor**](/uwp/api/Windows.Devices.Usb.UsbDescriptor) 对象表示的描述符的数组。 **UsbDescriptor**对象允许应用获取缓冲区中的描述符数据。 [**UsbDescriptor. DescriptorType**](/uwp/api/Windows.Devices.Usb.UsbDescriptor#Windows_Devices_Usb_UsbDescriptor_DescriptorType) 和 [**UsbDescriptor**](/uwp/api/Windows.Devices.Usb.UsbDescriptor#Windows_Devices_Usb_UsbDescriptor_Length) 属性存储保存描述符所需的缓冲区的类型和长度。

**注意**   所有描述符缓冲区的前两个字节还指示描述符的类型和长度。

 

例如， [**UsbConfiguration**](/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_Descriptors) 属性获取完整配置描述符的数组， (固定长度和可变长度部分) 。 该数组中的第一个元素是固定长度的配置描述符 (与 [**UsbConfigurationDescriptor**](/uwp/api/Windows.Devices.Usb.UsbConfigurationDescriptor)) 相同，第二个元素是第一个备用设置的接口描述符，依此类推。

同样， [**UsbInterface**](/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_Descriptors) 属性获取所有接口描述符和相关终结点描述符的数组。 [**UsbInterfaceSetting**](/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_Descriptors)属性获取该设置的所有描述符（如终结点描述符）的数组。

当应用程序想要检索自定义描述符或其他描述符（如 SuperSpeed 设备的终结点伴随描述符）时，这种获取描述符的方法非常有用。

此代码示例演示如何从配置描述符获取缓冲区中的描述符数据。 该示例获取配置描述符集，并分析该集中包含的所有描述符。 对于每个描述符，它使用 DataReader 对象读取缓冲区，并显示描述符长度和类型。 可以获取自定义描述符，如本示例中所示。

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

 

