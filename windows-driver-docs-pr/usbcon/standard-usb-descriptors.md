---
Description: USB 设备在称为 USB 描述符的数据结构中提供自身的相关信息。 本部分提供有关设备、配置、接口和终结点描述符以及从 USB 设备检索它们的方法的信息。
title: 标准 USB 描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b951b8f4ad092e35627b6bb983a47b3f72e6ccd0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824167"
---
# <a name="standard-usb-descriptors"></a>标准 USB 描述符


**摘要**

-   USB 描述符的类型
-   用于 USB 检索描述符的 Microsoft 提供的编程接口

**重要的 API**

-   请参阅本主题中包含的引用表。

USB 设备在称为*USB 描述符*的数据结构中提供自身的相关信息。 本部分提供有关设备、配置、接口和终结点描述符以及从 USB 设备检索它们的方法的信息。

## <a name="usb-descriptors-mapped-to-device-layout"></a>映射到设备布局的 USB 描述符


主机软件通过向默认终结点发送各种标准控制请求来从连接的设备中获取描述符（获取描述符请求，请参阅 USB 规范部分9.4.3）。 这些请求指定要检索的描述符类型。 为响应此类请求，设备会发送包含有关设备、其配置、接口和相关终结点的信息的描述符。 *设备描述符*包含有关整个设备的信息。 *配置描述符*包含有关每个设备配置的信息。 *字符串描述符*包含 Unicode 文本字符串。

每个 USB 设备都公开一个设备描述符，用于指示设备的类信息、供应商和产品标识符，以及配置数。 每个配置都公开其配置描述符，以指示接口和电源特征的数目。 每个接口都公开其每个替代设置的接口描述符，其中包含有关类的信息和终结点的数目。 每个接口中的每个终结点都公开终结点描述符，指示终结点类型和最大数据包大小。

例如，假设 OSR FX2 板设备布局（请参阅 USB 设备布局）。 在设备级别，设备将公开默认终结点的设备描述符和终结点描述符。 在配置级别，设备会为配置0公开配置描述符。 在接口级别，它为备用设置0公开了一个接口描述符。 在终结点级别，它公开了三个终结点说明符。

![usb 设备描述符布局](images/device-descriptors.png)

## <a name="usb-device-descriptor"></a>USB 设备描述符


每个通用串行总线（USB）设备必须能够提供单个设备描述符，其中包含有关设备的相关信息。 Windows 使用该信息来派生各种信息集。 例如，" **idVendor** " 和 " **idProduct** " 字段分别指定供应商和产品标识符。 Windows 使用这些字段值来构造设备的硬件 ID。 若要查看特定设备的硬件 ID，请打开设备管理器并查看设备属性。 在 "**详细信息**" 选项卡中，"**硬件 id** " 属性值表示 WINDOWS 生成的硬件 id （"USB\\XXX"）。 **BcdUSB**字段指示设备符合的 USB 规范的版本。 例如，0x0200 指示设备按照 USB 2.0 规范设计。 **BcdDevice**值指示设备定义的修订号。 USB 驱动程序堆栈使用**bcdDevice**以及**idVendor**和**idProduct**来生成设备的硬件和兼容 id。 可以在设备管理器中查看这些标识符。 设备描述符还表明设备支持的配置总数。

宿主通过控件传输获取设备描述符。 Microsoft 提供了用于获取描述符的编程接口。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>如果正在编写 。</th>
<th>调用 。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用<a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb" data-raw-source="[&lt;strong&gt;Windows.Devices.Usb&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)"> <strong>Windows USB</strong>的 UWP 应用</a></td>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DeviceDescriptor" data-raw-source="[&lt;strong&gt;UsbDevice.DeviceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DeviceDescriptor)"><strong>UsbDevice.DeviceDescriptor</strong></a></td>
</tr>
<tr class="even">
<td>使用<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb" data-raw-source="[WinUSB Functions](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)">WinUSB 函数</a>的 Win32 桌面应用</td>
<td><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor)"><strong>WinUsb_GetDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>基于 UMDF 的客户端驱动程序</td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::RetrieveDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor)"><strong>IWDFUsbTargetDevice::RetrieveDescriptor</strong></a></td>
</tr>
<tr class="even">
<td>基于 KMDF 的客户端驱动程序</td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceGetDeviceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor)"><strong>WdfUsbTargetDeviceGetDeviceDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>基于 WDM 的客户端驱动程序</td>
<td><a href="https://docs.microsoft.com/previous-versions/ff538943(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85))"><strong>UsbBuildGetDescriptorRequest</strong></a>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_descriptor_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_descriptor_request)"><strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong></a></p></td>
</tr>
</tbody>
</table>

 

## <a name="usb-configuration-descriptor"></a>USB 配置描述符


USB 配置包含一系列接口。 每个接口都包含一个或多个备用设置，每个备用设置由一组终结点组成（请参阅 USB 设备布局）。 配置描述符描述了整个配置，包括其接口、备用设置和终结点。 其中的每个实体还以其描述符格式进行描述。 配置描述符还可以包括由设备制造商定义的自定义描述符。

因此，只有配置描述符的初始部分是固定的，9个字节。 Rest 是可变的，具体取决于接口的数量及其备用设置，以及设备支持的终结点。 在此文档集中，初始9个字节称为配置描述符。 描述符的前两个字节指示总长度。

以下示例显示了 USB 网络摄像机设备的配置描述符：

``` syntax
Configuration Descriptor:
wTotalLength:         0x02CA
bNumInterfaces:       0x02
bConfigurationValue:  0x01
iConfiguration:       0x00
bmAttributes:         0x80 (Bus Powered )
MaxPower:             0xFA (500 mA)
```

**BConfigurationValue**字段指示设备固件中定义的配置的编号。 USB 配置还指示某些电源特征。 **BmAttributes**包含一个位掩码，该位掩码指示配置是否支持远程唤醒功能，以及设备是由总线供电还是自供电。 **MaxPower**字段指定设备在总线供电时可以从主机中抽取的最大电量（以 milliamp 单位）。 该配置描述符还指示设备支持的接口（**bNumInterfaces**）的总数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>如果正在编写 。</th>
<th>调用 。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用<a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb" data-raw-source="[&lt;strong&gt;Windows.Devices.Usb&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)"> <strong>Windows USB</strong>的 UWP 应用</a></td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfigurationDescriptor" data-raw-source="[&lt;strong&gt;UsbDevice.ConfigurationDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfigurationDescriptor)"><strong>UsbDevice ConfigurationDescriptor</strong></a>获取固定长度部分。</p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors" data-raw-source="[&lt;strong&gt;UsbConfiguration.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors)"><strong>UsbConfiguration</strong></a>获取整个配置集。</p></td>
</tr>
<tr class="even">
<td>使用<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb" data-raw-source="[WinUSB Functions](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)">WinUSB 函数</a>的 Win32 桌面应用</td>
<td><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor)"><strong>WinUsb_GetDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>基于 UMDF 的客户端驱动程序</td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::RetrieveDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor)"><strong>IWDFUsbTargetDevice::RetrieveDescriptor</strong></a></td>
</tr>
<tr class="even">
<td>基于 KMDF 的客户端驱动程序</td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceRetrieveConfigDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)"><strong>WdfUsbTargetDeviceRetrieveConfigDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>基于 WDM 的客户端驱动程序</td>
<td><p><a href="https://docs.microsoft.com/previous-versions/ff538943(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85))"><strong>UsbBuildGetDescriptorRequest</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_configuration_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_CONFIGURATION_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_configuration_request)"><strong>_URB_CONTROL_GET_CONFIGURATION_REQUEST</strong></a></p></td>
</tr>
</tbody>
</table>

 

## <a name="usb-interface-descriptor"></a>USB 接口描述符


接口描述符包含有关 USB 接口的替代设置的信息。

以下示例显示了用于网络摄像机设备的接口0的备用设置0的接口描述符：

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

在前面的示例中，请注意**bInterfaceNumber**和**bAlternateSetting**字段的值。 这些字段包含索引值，主机使用这些值来激活接口及其备用设置之一。 对于激活，应用程序或驱动程序会在函数调用中指定索引值。 根据该信息，USB 驱动程序堆栈会构建标准控制请求（设置接口）并将其发送到设备。 请注意 " **bInterfaceClass** " 字段。 接口描述符或它的任何备用设置的描述符指定类代码、子类和协议。 0x0E 的值指示接口适用于视频设备类。 另外，请注意**iInterface**字段。 该值指示在接口描述符后面追加了两个字符串说明符。 字符串描述符包含在设备枚举过程中用来标识功能的 Unicode 说明。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>如果正在编写 。</th>
<th>调用 。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用<a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb" data-raw-source="[&lt;strong&gt;Windows.Devices.Usb&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)"> <strong>Windows USB</strong>的 UWP 应用</a></td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_Descriptors" data-raw-source="[&lt;strong&gt;UsbInterfaceSetting.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_Descriptors)"><strong>UsbInterfaceSetting</strong></a>获取特定备用设置的特定描述符。</p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_Descriptors" data-raw-source="[&lt;strong&gt;UsbInterface.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_Descriptors)"><strong>UsbInterface</strong></a>获取接口的所有设置的描述符。</p></td>
</tr>
<tr class="even">
<td>使用<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb" data-raw-source="[WinUSB Functions](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)">WinUSB 函数</a>的 Win32 桌面应用</td>
<td><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor)"><strong>WinUsb_GetDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>基于 UMDF 的客户端驱动程序</td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacedescriptor" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::GetInterfaceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacedescriptor)"><strong>IWDFUsbInterface::GetInterfaceDescriptor</strong></a></td>
</tr>
<tr class="even">
<td>基于 KMDF 的客户端驱动程序</td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetdescriptor" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetdescriptor)"><strong>WdfUsbInterfaceGetDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>基于 WDM 的客户端驱动程序</td>
<td><p><a href="https://docs.microsoft.com/previous-versions/ff538943(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85))"><strong>UsbBuildGetDescriptorRequest</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_configuration_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_CONFIGURATION_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_configuration_request)"><strong>_URB_CONTROL_GET_CONFIGURATION_REQUEST</strong></a> ，然后分析每个接口描述符。 有关详细信息，请参阅<a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">如何为 USB 设备选择配置</a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="usb-endpoint-descriptor"></a>USB 终结点描述符


接口中的每个终结点都描述了设备的单个输入或输出流。 支持不同类型的函数的流的设备有多个接口。 支持多个与函数相关的流的设备可支持单个接口上的多个终结点。

所有类型的终结点（默认终结点除外）都必须提供终结点描述符，以便宿主可以获取有关终结点的信息。 终结点描述符包含信息，例如其地址、类型、方向和终结点可以处理的数据量。 传输到终结点的数据基于该信息。

以下示例显示了网络摄像机设备的终结点描述符：

``` syntax
Endpoint Descriptor:
bEndpointAddress:   0x82  IN
bmAttributes:       0x01
wMaxPacketSize:     0x0080 (128)
bInterval:          0x01
```

**BEndpointAddress**字段指定包含终结点编号（位 3. 0）和终结点（第7位）方向的唯一终结点地址。 通过读取前面的示例中的这些值，可以确定该描述符在终结点（其终结点号为2）中进行了说明。 **BmAttributes**特性指示终结点类型为 "同步"。 **WMaxPacketSizefield**指示终结点可以在单个事务中发送或接收的最大字节数。 第12位. 11 表示每个 microframe 可发送的事务总数。 **BInterval**指示终结点可以发送或接收数据的频率。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>如果正在编写 。</th>
<th>调用 。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用<a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb" data-raw-source="[&lt;strong&gt;Windows.Devices.Usb&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)"> <strong>Windows USB</strong>的 UWP 应用</a></td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbEndpointDescriptor" data-raw-source="[&lt;strong&gt;UsbEndpointDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbEndpointDescriptor)"><strong>UsbEndpointDescriptor</strong></a></p></td>
</tr>
<tr class="even">
<td>使用<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb" data-raw-source="[WinUSB Functions](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)">WinUSB 函数</a>的 Win32 桌面应用</td>
<td><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor)"><strong>WinUsb_GetDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>基于 UMDF 的客户端驱动程序</td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-getinformation" data-raw-source="[&lt;strong&gt;WDFUsbTargetPipe::GetInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-getinformation)"><strong>WDFUsbTargetPipe：： GetInformation</strong></a></td>
</tr>
<tr class="even">
<td>基于 KMDF 的客户端驱动程序</td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeGetInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation)"><strong>WdfUsbTargetPipeGetInformation</strong></a></td>
</tr>
<tr class="odd">
<td>基于 WDM 的客户端驱动程序</td>
<td><p><a href="https://docs.microsoft.com/previous-versions/ff538943(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85))"><strong>UsbBuildGetDescriptorRequest</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_configuration_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_CONFIGURATION_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_configuration_request)"><strong>_URB_CONTROL_GET_CONFIGURATION_REQUEST</strong></a> ，然后针对每个终结点描述符进行分析。 有关详细信息，请参阅<a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">如何为 USB 设备选择配置</a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[所有 USB 开发人员的概念](usb-concepts-for-all-developers.md)  



