---
Description: A USB device provides information about itself in data structures called USB descriptors. This section provides information about device, configuration, interface, and endpoint descriptors and ways to retrieve them from a USB device.
title: 标准 USB 描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d72b445cd88a078b261dfcdee731338b8e332bcc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540480"
---
# <a name="standard-usb-descriptors"></a>标准 USB 描述符


**摘要**

-   USB 描述符类型
-   Microsoft 提供的编程接口的 USB 检索描述符

**重要的 Api**

-   请参阅本主题中包含的引用表。

USB 设备提供了有关其自身在名为的数据结构中的信息*USB 描述符*。 本部分提供有关设备、 配置、 接口和终结点描述符和方法从 USB 设备中检索信息。

## <a name="usb-descriptors-mapped-to-device-layout"></a>映射到设备布局的 USB 描述符


主机软件将各种标准控件请求发送到默认终结点 （Get 描述符请求，请参阅 USB 规范部分 9.4.3） 从已连接的设备上获取描述符。 这些请求指定的类型描述符来检索。 此类请求的响应，设备发送描述符包括有关设备、 其配置、 接口和相关的终结点的信息。 *设备描述符*包含整个设备的相关信息。 *配置描述符*包含有关每个设备配置信息。 *字符串描述符*包含 Unicode 文本字符串。

每个 USB 设备公开的设备描述符，指示设备的类信息、 供应商和产品标识符，以及多个配置。 每个配置还公开其配置描述符，该值指示大量接口和功耗特征。 每个接口公开其包含类和数量的终结点信息的替代设置的每个接口描述符。 每个接口中的每个终结点公开终结点，描述符可指明终结点类型和最大数据包大小。

例如，让我们考虑 OSR FX2 看板设备布局 （请参阅 USB 设备布局）。 在设备级别，设备会公开设备描述符和默认终结点的终结点描述符。 在配置级别，设备配置 0 公开配置描述符。 在接口级别，它公开一个接口描述符为备用设置 0。 为终结点级别，它公开三个终结点描述符。

![usb 设备描述符布局](images/device-descriptors.png)

## <a name="usb-device-descriptor"></a>USB 设备描述符


每个通用串行总线 (USB) 设备必须能够提供包含有关设备的相关信息的单个设备描述符。 Windows 使用该信息来派生不同组的信息。 例如， **idVendor**并**idProduct**字段分别指定供应商和产品标识符。 Windows 使用这些字段值来构造该设备的硬件 ID。 若要查看特定设备的硬件 ID，请打开设备管理器并查看设备属性。 在中**详细信息**选项卡上，**硬件 Id**属性值指示的硬件 ID ("USB\\XXX") 生成的 Windows。 **BcdUSB**字段指示设备是否符合的 USB 规范的版本。 例如，0x0200 指示该设备的设计根据 USB 2.0 规范。 **BcdDevice**值指示设备定义修订号。 使用 USB 驱动程序堆栈**bcdDevice**，连同**idVendor**并**idProduct**，以便生成硬件和设备兼容 Id。 您可以查看与设备管理器中的标识符。 设备描述符还指示设备支持的配置的总数。

获得通过控制传输的设备描述符。 Microsoft 提供了编程接口，以获取描述符。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>如果你正在编写...</th>
<th>调用...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用 UWP 应用<a href="https://msdn.microsoft.com/library/windows/apps/dn278466" data-raw-source="[&lt;strong&gt;Windows.Devices.Usb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278466)"> <strong>Windows.Devices.Usb</strong></a></td>
<td><a href="https://msdn.microsoft.com/library/windows/apps/dn264002" data-raw-source="[&lt;strong&gt;UsbDevice.DeviceDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264002)"><strong>UsbDevice.DeviceDescriptor</strong></a></td>
</tr>
<tr class="even">
<td>Win32 桌面应用，通过<a href="https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb" data-raw-source="[WinUSB Functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)">WinUSB 函数</a></td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff540257" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540257)"><strong>WinUsb_GetDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>UMDF 基于客户端驱动程序</td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff560374" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::RetrieveDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560374)"><strong>IWDFUsbTargetDevice::RetrieveDescriptor</strong></a></td>
</tr>
<tr class="even">
<td>KMDF 基于客户端驱动程序</td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff550090" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceGetDeviceDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550090)"><strong>WdfUsbTargetDeviceGetDeviceDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>WDM 基于客户端驱动程序</td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff538943" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538943)"><strong>UsbBuildGetDescriptorRequest</strong></a>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540357" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540357)"><strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong></a></p></td>
</tr>
</tbody>
</table>

 

## <a name="usb-configuration-descriptor"></a>USB 配置描述符


USB 配置包含一系列的接口。 每个接口由一个或多个备用的设置，和每个备用设置由一组终结点 （请参阅 USB 设备布局） 组成。 配置说明符所描述的整个配置包括它的接口、 替代设置和其终结点。 每个实体还介绍了在其描述符格式。 配置描述符还可以包括由设备制造商定义的自定义描述符。

因此，仅配置描述符的初始部分被固定的为 9 个字节。 其余部分是根据接口及其替代设置和设备支持的终结点的数量的变量。 在此文档集，初始的 9 个字节被称为配置描述符。 描述符的前两个字节表示的总长度。

下面的示例显示了 USB 网络摄像机设备的配置描述符：

``` syntax
Configuration Descriptor:
wTotalLength:         0x02CA
bNumInterfaces:       0x02
bConfigurationValue:  0x01
iConfiguration:       0x00
bmAttributes:         0x80 (Bus Powered )
MaxPower:             0xFA (500 mA)
```

**BConfigurationValue**字段指示设备的固件中定义的配置的编号。 USB 配置还指示某些 power 特征。 **BmAttributes**包含一个位掩码，指示配置是否支持远程唤醒功能，以及设备是总线供电还是自供电。 **MaxPower**字段指定打开设备时是总线的设备可以从主机中，绘制的最大功率 （以 milliamp 为单位）。 配置描述符还指示接口的总数 (**bNumInterfaces**) 的设备支持。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>如果你正在编写...</th>
<th>调用...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用 UWP 应用<a href="https://msdn.microsoft.com/library/windows/apps/dn278466" data-raw-source="[&lt;strong&gt;Windows.Devices.Usb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278466)"> <strong>Windows.Devices.Usb</strong></a></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/apps/dn297689" data-raw-source="[&lt;strong&gt;UsbDevice.ConfigurationDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn297689)"><strong>UsbDevice.ConfigurationDescriptor</strong> </a>若要获取的固定的长度部分。</p>
<p><a href="https://msdn.microsoft.com/library/windows/apps/dn263802" data-raw-source="[&lt;strong&gt;UsbConfiguration.Descriptors&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn263802)"><strong>UsbConfiguration.Descriptors</strong> </a>获取整个配置集。</p></td>
</tr>
<tr class="even">
<td>Win32 桌面应用，通过<a href="https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb" data-raw-source="[WinUSB Functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)">WinUSB 函数</a></td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff540257" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540257)"><strong>WinUsb_GetDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>UMDF 基于客户端驱动程序</td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff560374" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::RetrieveDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560374)"><strong>IWDFUsbTargetDevice::RetrieveDescriptor</strong></a></td>
</tr>
<tr class="even">
<td>KMDF 基于客户端驱动程序</td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff550098" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceRetrieveConfigDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550098)"><strong>WdfUsbTargetDeviceRetrieveConfigDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>WDM 基于客户端驱动程序</td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538943" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538943)"><strong>UsbBuildGetDescriptorRequest</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540365" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_CONFIGURATION_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540365)"><strong>_URB_CONTROL_GET_CONFIGURATION_REQUEST</strong></a></p></td>
</tr>
</tbody>
</table>

 

## <a name="usb-interface-descriptor"></a>USB 接口描述符


接口描述符包含 USB 接口的一项备用设置有关的信息。

下面的示例演示为备用设置 0 的网络摄像机设备接口 0 接口描述符：

``` syntax
Interface Descriptor:
bInterfaceNumber:     0x00
bAlternateSetting:    0x00
bNumEndpoints:        0x01
bInterfaceClass:      0x0E
bInterfaceSubClass:   0x02
bInterfaceProtocol:   0x00
iInterface:           0x02
0x0409: "Microsoft LifeCam VX-5000"
0x0409: "Microsoft LifeCam VX-5000"
```

在前面的示例，请注意**bInterfaceNumber**并**bAlternateSetting**字段值。 这些字段包含主机用于激活的接口和一个其替代设置的索引值。 用于激活、 情况下，应用程序或驱动程序指定的索引值的函数调用中。 USB 驱动程序堆栈基于该信息，然后生成标准控件请求 （设置接口） 并将其发送到设备。 请注意**bInterfaceClass**字段。 接口描述符或任何其替代设置描述符指定的类代码、 子类和协议。 0x0E 的值指示该接口是视频设备类。 另请注意**iInterface**字段。 该值指示两个字符串描述符附加到接口描述符。 字符串描述符包含 Unicode 在设备枚举过程中用于标识功能的说明。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>如果你正在编写...</th>
<th>调用...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用 UWP 应用<a href="https://msdn.microsoft.com/library/windows/apps/dn278466" data-raw-source="[&lt;strong&gt;Windows.Devices.Usb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278466)"> <strong>Windows.Devices.Usb</strong></a></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/apps/dn264281" data-raw-source="[&lt;strong&gt;UsbInterfaceSetting.Descriptors&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264281)"><strong>UsbInterfaceSetting.Descriptors</strong> </a>来获取特定的替代设置的特定的描述符。</p>
<p><a href="https://msdn.microsoft.com/library/windows/apps/dn264281" data-raw-source="[&lt;strong&gt;UsbInterface.Descriptors&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264281)"><strong>UsbInterface.Descriptors</strong> </a>获取描述符的接口的所有设置。</p></td>
</tr>
<tr class="even">
<td>Win32 桌面应用，通过<a href="https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb" data-raw-source="[WinUSB Functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)">WinUSB 函数</a></td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff540257" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540257)"><strong>WinUsb_GetDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>UMDF 基于客户端驱动程序</td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff560320" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::GetInterfaceDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560320)"><strong>IWDFUsbInterface::GetInterfaceDescriptor</strong></a></td>
</tr>
<tr class="even">
<td>KMDF 基于客户端驱动程序</td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff550060" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550060)"><strong>WdfUsbInterfaceGetDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>WDM 基于客户端驱动程序</td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538943" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538943)"><strong>UsbBuildGetDescriptorRequest</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540365" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_CONFIGURATION_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540365)"><strong>_URB_CONTROL_GET_CONFIGURATION_REQUEST</strong> </a> ，然后分析为每个接口描述符。 有关详细信息，请参阅<a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">如何为 USB 设备选择一个配置</a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="usb-endpoint-descriptor"></a>USB 终结点描述符


每个终结点，接口中的描述的输入或输出设备的单个流。 为不同类型的函数支持流的设备有多个接口。 支持适用于函数的几个流的设备可以在单个接口上支持多个终结点。

所有类型的终结点 （除默认终结点） 必须都提供终结点描述符，以便主机可以获取有关终结点的信息。 终结点描述符包括信息，例如其地址、 类型、 方向，并可以处理终结点的数据量。 将数据传输至终结点基于该信息。

下面的示例显示了网络摄像头设备的终结点描述符：

``` syntax
Endpoint Descriptor:
bEndpointAddress:   0x82  IN
bmAttributes:       0x01
wMaxPacketSize:     0x0080 (128)
bInterval:          0x01
```

**BEndpointAddress**字段指定包含终结点号 (位 3..0) 和终结点 (位 7) 的方向的唯一的终结点地址。 通过阅读这些值在前面的示例，我们可以确定描述符描述其终结点号为 2 的在终结点。 **BmAttributes**属性指示终结点类型为等时。 **WMaxPacketSizefield**指示最大字节数的终结点可以发送或接收在单个事务中。 位 12..11 指示可以每 microframe 发送的事务总数。 **BInterval**指示终结点发送或接收数据的频率。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>如果你正在编写...</th>
<th>调用...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用 UWP 应用<a href="https://msdn.microsoft.com/library/windows/apps/dn278466" data-raw-source="[&lt;strong&gt;Windows.Devices.Usb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278466)"> <strong>Windows.Devices.Usb</strong></a></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/apps/dn264052" data-raw-source="[&lt;strong&gt;UsbEndpointDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264052)"><strong>UsbEndpointDescriptor</strong></a></p></td>
</tr>
<tr class="even">
<td>Win32 桌面应用，通过<a href="https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb" data-raw-source="[WinUSB Functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)">WinUSB 函数</a></td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff540257" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540257)"><strong>WinUsb_GetDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>UMDF 基于客户端驱动程序</td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff560403" data-raw-source="[&lt;strong&gt;WDFUsbTargetPipe::GetInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560403)"><strong>WDFUsbTargetPipe::GetInformation</strong></a></td>
</tr>
<tr class="even">
<td>KMDF 基于客户端驱动程序</td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff551142" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeGetInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551142)"><strong>WdfUsbTargetPipeGetInformation</strong></a></td>
</tr>
<tr class="odd">
<td>WDM 基于客户端驱动程序</td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538943" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538943)"><strong>UsbBuildGetDescriptorRequest</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540365" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_CONFIGURATION_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540365)"><strong>_URB_CONTROL_GET_CONFIGURATION_REQUEST</strong> </a> ，然后分析为每个终结点描述符。 有关详细信息，请参阅<a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">如何为 USB 设备选择一个配置</a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[所有 USB 开发人员的概念](usb-concepts-for-all-developers.md)  



