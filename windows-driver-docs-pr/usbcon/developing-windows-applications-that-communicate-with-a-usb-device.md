---
Description: 本主题提供指南以决定是否应编写的 UWP 应用或 Windows 桌面应用程序与 USB 设备进行通信。
title: 为 USB 设备开发 Windows 应用程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa265fd6af08b8d8ea8bb64617256acbc2f3a3e4
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394035"
---
# <a name="developing-windows-applications-for-usb-devices"></a>为 USB 设备开发 Windows 应用程序


**摘要**

-   选择正确的编程模式的准则
-   UWP 应用和桌面应用开发人员体验

**重要的 API**

-   [**Windows.Devices.Usb**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)
-   [WinUSB 函数](using-winusb-api-to-communicate-with-a-usb-device.md)

本主题提供指南以决定是否应编写的 UWP 应用或 Windows 桌面应用程序与 USB 设备进行通信。

Windows 提供了可用于编写与自定义的 USB 设备的应用程序的 API 集。 API 执行常见 USB 相关的任务，例如，查找设备、 数据传输。

在此上下文中的"自定义设备"意味着，Microsoft 不提供内置类驱动程序的设备。 相反，你可以安装 WinUSB (Winusb.sys) 作为设备驱动程序。

## <a name="choosing-a-programming-model"></a>选择编程模型


如果您在安装[Winusb.sys](winusb-installation.md)，编程模型选项如下：

-   [USB 设备的 UWP 应用](writing-usb-device-companion-apps-for-microsoft-store.md)

    Windows 8.1 提供了新的命名空间：[**Windows.Devices.Usb**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)。 不能在早期版本的 Windows 中使用的命名空间。 此处是 Microsoft Store 中的其他资源：[UWP 应用](https://msdn.microsoft.com/windows/apps)。

-   [有关 USB 设备的 Windows 桌面应用程序](windows-desktop-app-for-a-usb-device.md)

    Windows 8.1，已通过进行通信的应用程序之前[Winusb.sys](winusb-installation.md)，则是通过使用编写桌面应用程序[WinUSB 函数](using-winusb-api-to-communicate-with-a-usb-device.md)。 在 Windows 8.1 API 集已扩展。 目前 Windows 桌面应用程序的其他资源：[Windows 桌面应用程序](https://developer.microsoft.com/windows/desktop)。

选择编程模型的最佳的策略取决于各种因素。

-   **将您的应用程序会与其内部的 USB 设备？**

    Api 的主要设计用于访问外围设备。 API 还可以访问 PC 内部的 USB 设备。 但是从 UWP 应用访问 PC 内部的 USB 设备是有限的特权的应用程序中显式声明的设备元数据由 OEM 该电脑。

-   **将您的应用程序会与其 USB 等时终结点？**

    如果您的应用程序传输到或从设备的同步终结点的数据，必须编写一个 Windows 桌面应用程序。 在新的 Windows 8.1 [WinUSB 函数](using-winusb-api-to-communicate-with-a-usb-device.md)已添加到允许桌面应用程序将数据发送到和从同步终结点接收数据的 API 集。

-   **是您的应用程序"控制面板"类型？**

    UWP 应用是每用户应用程序，但没有超出了每个应用的范围进行的更改的功能。 对于这些类型的应用程序，必须编写一个 Windows 桌面应用程序。

-   **USB 设备是否通过 UWP 应用的支持类类？**

    如果你的设备属于某个这些设备类的情况下编写的 UWP 应用。

    -   `name:cdcControl,           classId:02 * *`
    -   `name:physical, classId:05 * *`
    -   `name:personalHealthcare,   classId:0f 00 00`
    -   `name:activeSync,           classId:ef 01 01`
    -   `name:palmSync,             classId:ef 01 02`
    -   `name:deviceFirmwareUpdate, classId:fe 01 01`
    -   `name:irda,                 classId:fe 02 00     `
    -   `name:measurement,          classId:fe 03 *`
    -   `name:vendorSpecific,       classId:ff * *`

    **请注意**如果你的设备属于 DeviceFirmwareUpdate 类，您的应用程序必须为特权的应用程序。




如果你的设备不属于其中一个前面的设备类，编写的 Windows 桌面应用。


## <a name="driver-requirement"></a>驱动程序要求


| 驱动程序要求 | UWP 应用                                                                                                                          | Windows 桌面应用程序                                                                                                                       |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| 功能驱动程序    | Microsoft 提供[Winusb.sys](winusb-installation.md) （内核模式驱动程序）。                                                             | Microsoft 提供[Winusb.sys](winusb-installation.md) （内核模式驱动程序）。                                                            |
| 筛选器驱动程序      | 如果筛选器驱动程序存在，请访问仅限于特权的应用程序。 由 OEM 情况下，应用程序声明为特权的应用程序中的设备元数据。 | 只要它不会阻止访问筛选器驱动程序可出现在内核模式设备堆栈[Winusb.sys](winusb-installation.md)。 |



## <a name="code-samples"></a>代码示例


<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>示例</th>
<th>UWP 应用</th>
<th>Windows 桌面应用程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>这些示例入门</td>
<td><ul>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[Custom USB device access sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">自定义的 USB 设备访问示例</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[USB CDC Control sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">USB CDC 控制示例</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[Firmware Update USB Device sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">固件更新 USB 设备示例</a></li>
</ul></td>
<td><ul>
<li>开头<strong>WinUsb 应用程序</strong>（Ultimate 或 Professional） Microsoft Visual Studio 附带的模板</li>
<li>使用代码示例中所示扩展模板<a href="using-winusb-api-to-communicate-with-a-usb-device.md" data-raw-source="[How to Access a USB Device by Using WinUSB Functions](using-winusb-api-to-communicate-with-a-usb-device.md)">如何访问由使用 WinUSB 函数 USB 设备</a>。</li>
</ul></td>
</tr>
</tbody>
</table>



## <a name="development-tools"></a>开发工具


<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>开发工具</th>
<th>UWP 应用</th>
<th>Windows 桌面应用程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>开发人员环境</td>
<td><p>Microsoft Visual Studio 2013</p>
<p>对于 Windows 8.1 的 Microsoft Windows 软件开发工具包 (SDK)</p></td>
<td><p>使用<strong>WinUSB 应用程序</strong>模板包括在 Visual Studio （Ultimate 或 Professional） 和 Windows Driver Kit (WDK) 8</p>
<div class="alert">
<strong>请注意</strong>对同步传输，Visual Studio 2013 与 Windows Driver Kit (WDK) 8.1
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td>编程语言</td>
<td>C#VB.NET， C++，JavaScript</td>
<td>C/C++</td>
</tr>
</tbody>
</table>



## <a name="feature-implementation"></a>功能实现


<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>关键方案</th>
<th>UWP 应用</th>
<th>Windows 桌面应用程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>设备发现</td>
<td>使用<a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration" data-raw-source="[&lt;strong&gt;Windows.Devices.Enumeration&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration)"> <strong>Windows.Devices.Enumeration</strong> </a>命名空间获取<a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice" data-raw-source="[&lt;strong&gt;UsbDevice&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice)"> <strong>UsbDevice</strong></a>。</td>
<td>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/install/setupapi" data-raw-source="[SetupAPI](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi)">SetupAPI</a>函数和<a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize" data-raw-source="[&lt;strong&gt;WinUsb_Initialize&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize)"> <strong>WinUsb_Initialize</strong> </a>获取 WINUSB_INTERFACE_HANDLE。</td>
</tr>
<tr class="even">
<td>USB 控制传输</td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbSetupPacket" data-raw-source="[&lt;strong&gt;UsbSetupPacket&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbSetupPacket)"><strong>UsbSetupPacket</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbControlRequestType" data-raw-source="[&lt;strong&gt;UsbControlRequestType&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbControlRequestType)"><strong>UsbControlRequestType</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlInTransferAsync_Windows_Devices_Usb_UsbSetupPacket_Windows_Storage_Streams_IBuffer_" data-raw-source="[&lt;strong&gt;UsbDevice.SendControlInTransferAsync&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlInTransferAsync_Windows_Devices_Usb_UsbSetupPacket_Windows_Storage_Streams_IBuffer_)"><strong>UsbDevice.SendControlInTransferAsync</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlOutTransferAsync_Windows_Devices_Usb_UsbSetupPacket_" data-raw-source="[&lt;strong&gt;UsbDevice.SendControlOutTransferAsync&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlOutTransferAsync_Windows_Devices_Usb_UsbSetupPacket_)"><strong>UsbDevice.SendControlOutTransferAsync</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/ns-winusb-_winusb_setup_packet" data-raw-source="[&lt;strong&gt;WINUSB_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/ns-winusb-_winusb_setup_packet)"><strong>WINUSB_SETUP_PACKET</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer" data-raw-source="[&lt;strong&gt;WinUsb_ControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer)"><strong>WinUsb_ControlTransfer</strong></a></p></td>
</tr>
<tr class="odd">
<td>获取 USB 描述符</td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DeviceDescriptor" data-raw-source="[&lt;strong&gt;UsbDevice.DeviceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DeviceDescriptor)"><strong>UsbDevice.DeviceDescriptor</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors" data-raw-source="[&lt;strong&gt;UsbConfiguration.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors)"><strong>UsbConfiguration.Descriptors</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_Descriptors" data-raw-source="[&lt;strong&gt;UsbInterface.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_Descriptors)"><strong>UsbInterface.Descriptors</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbEndpointDescriptor" data-raw-source="[&lt;strong&gt;UsbEndpointDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbEndpointDescriptor)"><strong>UsbEndpointDescriptor</strong></a></p></td>
<td><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor)"><strong>WinUsb_GetDescriptor</strong></a></td>
</tr>
<tr class="even">
<td>发送 USB 大容量传输</td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe" data-raw-source="[&lt;strong&gt;UsbBulkInPipe&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe)"><strong>UsbBulkInPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe" data-raw-source="[&lt;strong&gt;UsbBulkOutPipe&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe)"><strong>UsbBulkOutPipe</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe" data-raw-source="[&lt;strong&gt;WinUsb_ReadPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)"><strong>WinUsb_ReadPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe" data-raw-source="[&lt;strong&gt;WinUsb_WritePipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)"><strong>WinUsb_WritePipe</strong></a></p></td>
</tr>
<tr class="odd">
<td>发送 USB 中断传输</td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe" data-raw-source="[&lt;strong&gt;UsbInterruptInPipe&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe)"><strong>UsbInterruptInPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe" data-raw-source="[&lt;strong&gt;UsbInterruptOutPipe&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe)"><strong>UsbInterruptOutPipe</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe" data-raw-source="[&lt;strong&gt;WinUsb_ReadPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)"><strong>WinUsb_ReadPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe" data-raw-source="[&lt;strong&gt;WinUsb_WritePipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)"><strong>WinUsb_WritePipe</strong></a></p></td>
</tr>
<tr class="even">
<td>发送 USB 同步传输</td>
<td>不支持。</td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipe" data-raw-source="[&lt;strong&gt;WinUsb_ReadIsochPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipe)"><strong>WinUsb_ReadIsochPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap" data-raw-source="[&lt;strong&gt;WinUsb_ReadIsochPipeAsap&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap)"><strong>WinUsb_ReadIsochPipeAsap</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe" data-raw-source="[&lt;strong&gt;WinUsb_WriteIsochPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe)"><strong>WinUsb_WriteIsochPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap" data-raw-source="[&lt;strong&gt;WinUsb_WriteIsochPipeAsap&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap)"><strong>WinUsb_WriteIsochPipeAsap</strong></a></p></td>
</tr>
<tr class="odd">
<td>关闭设备</td>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_Close" data-raw-source="[&lt;strong&gt;UsbDevice.Close&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_Close)"><strong>UsbDevice.Close</strong></a></td>
<td><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free" data-raw-source="[&lt;strong&gt;WinUsb_Free&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free)"><strong>WinUsb_Free</strong></a></td>
</tr>
</tbody>
</table>



## <a name="documentation"></a>文档


| 文档     | UWP 应用                                                                     | Windows 桌面应用程序                                                                                           |
|-------------------|---------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| 编程指南 | [与 USB 设备，开始-完成](talking-to-usb-devices-start-to-finish.md) | [如何通过使用 WinUSB 函数访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md) |
| API 参考     | [**Windows.Devices.Usb**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)                              | [WinUSB 函数](using-winusb-api-to-communicate-with-a-usb-device.md)                                     |



## <a name="related-topics"></a>相关主题
[通用串行总线 (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  



