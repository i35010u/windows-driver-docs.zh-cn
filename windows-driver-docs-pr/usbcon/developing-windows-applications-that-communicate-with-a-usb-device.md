---
description: 本主题提供了一些准则，用于确定是应该编写 UWP 应用还是 Windows 桌面应用来与 USB 设备进行通信。
title: 为 USB 设备开发 Windows 应用程序的概述
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 28f3a8988f9fb228f50348a48eda28b19cd84b39
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010293"
---
# <a name="overview-of-developing-windows-applications-for-usb-devices"></a>为 USB 设备开发 Windows 应用程序的概述


**摘要**

-   选择正确编程模型的准则
-   UWP 应用和桌面应用开发人员体验

**重要的 API**

-   [**Windows.Devices.Usb**](/uwp/api/Windows.Devices.Usb)
-   [WinUSB 函数](using-winusb-api-to-communicate-with-a-usb-device.md)

本主题提供了一些准则，用于确定是应该编写 UWP 应用还是 Windows 桌面应用来与 USB 设备进行通信。

Windows 提供了 API 集，可用于编写与自定义 USB 设备通信的应用。 该 API 执行与 USB 相关的常见任务，例如查找设备和数据传输。

此上下文中的“自定义设备”指的是 Microsoft 不提供随机类驱动程序的设备。 可以改为安装 WinUSB (Winusb.sys) 作为设备驱动程序。

## <a name="choosing-a-programming-model"></a>选择编程模型


如果安装 [Winusb.sys](winusb-installation.md)，以下是编程模型选项：

-   [用于 USB 设备的 UWP 应用](writing-usb-device-companion-apps-for-microsoft-store.md)

    Windows 8.1 提供新的命名空间：[Windows.Devices.Usb  ](/uwp/api/Windows.Devices.Usb)。 该命名空间无法用于旧版本的 Windows。 以下是其他 Microsoft Store 资源：[UWP 应用](https://msdn.microsoft.com/windows/apps)。

-   [用于 USB 设备的 Windows 桌面应用](windows-desktop-app-for-a-usb-device.md)

    在 Windows 8.1 之前，通过 [Winusb.sys](winusb-installation.md) 通信的应用是使用 [WinUSB 函数](using-winusb-api-to-communicate-with-a-usb-device.md)编写的桌面应用。 在 Windows 8.1 中，扩展了 API 集。 以下是其他 Windows 桌面应用资源：[Windows 桌面应用](https://developer.microsoft.com/windows/desktop)。

选择最佳编程模型的策略取决于各种因素。

-   **应用会与内部 USB 设备通信吗？**

    这些 API 主要是为访问外围设备而设计的。 该 API 还可以访问电脑内部的 USB 设备。 但是，从 UWP 应用访问电脑内部 USB 设备仅限于该电脑的 OEM 在设备元数据中显式声明的特权应用。

-   **应用会与 USB 常时等量终结点通信吗？**

    如果应用与设备的常时等量终结点之间传入或传出数据，则必须编写一个 Windows 桌面应用。 在 Windows 8.1 中，已将新的 [WinUSB 函数](using-winusb-api-to-communicate-with-a-usb-device.md)添加到 API 集，从而允许桌面应用与常时等量终结点之间发送或接收数据。

-   **应用是“控制面板”类型的应用吗？**

    UWP 应用是每用户应用，不具备在每个应用的范围之外进行更改的能力。 对于这些类型的应用，必须编写 Windows 桌面应用。

-   **UWP 应用是否支持 USB 设备类？**

    如果设备属于这些设备类之一，则请编写一个 UWP 应用。

    -   `name:cdcControl,           classId:02 * *`
    -   `name:physical, classId:05 * *`
    -   `name:personalHealthcare,   classId:0f 00 00`
    -   `name:activeSync,           classId:ef 01 01`
    -   `name:palmSync,             classId:ef 01 02`
    -   `name:deviceFirmwareUpdate, classId:fe 01 01`
    -   `name:irda,                 classId:fe 02 00     `
    -   `name:measurement,          classId:fe 03 *`
    -   `name:vendorSpecific,       classId:ff * *`

    注意  ：如果设备属于 DeviceFirmwareUpdate 类，则应用必须是特权应用。




如果设备不属于上述设备类之一，则请编写 Windows 桌面应用。


## <a name="driver-requirement"></a>驱动程序要求


| 驱动程序要求 | UWP 应用                                                                                                                          | Windows 桌面应用                                                                                                                       |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| 函数驱动程序    | Microsoft 提供的 [Winusb.sys](winusb-installation.md)（内核模式驱动程序）。                                                             | Microsoft 提供的 [Winusb.sys](winusb-installation.md)（内核模式驱动程序）。                                                            |
| 筛选器驱动程序      | 如果存在筛选器驱动程序，则访问仅限于特权应用。 该应用由 OEM 在设备元数据中声明为特权应用。 | 只要筛选器驱动程序不阻止对 [Winusb.sys](winusb-installation.md) 的访问，它就可以存在于内核模式的设备堆栈中。 |



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
<th>Windows 桌面应用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>开始使用这些示例</td>
<td><ul>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[Custom USB device access sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">自定义 USB 设备访问示例</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[USB CDC Control sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">USB CDC 控件示例</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[Firmware Update USB Device sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">固件更新 USB 设备示例</a></li>
</ul></td>
<td><ul>
<li>从 Microsoft Visual Studio Ultimate 或 Microsoft Visual Studio Professional 附带的 WinUsb 应用程序模板开始</li>
<li>使用<a href="using-winusb-api-to-communicate-with-a-usb-device.md" data-raw-source="[How to Access a USB Device by Using WinUSB Functions](using-winusb-api-to-communicate-with-a-usb-device.md)">如何使用 WinUSB 函数访问 USB 设备</a>中显示的代码示例来扩展模板。</li>
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
<th>Windows 桌面应用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>开发人员环境</td>
<td><p>Microsoft Visual Studio 2013</p>
<p>适用于 Windows 8.1 的 Microsoft Windows 软件开发工具包 (SDK)</p></td>
<td><p>使用 Visual Studio Ultimate 或 Visual Studio Professional 以及 Windows 驱动程序工具包 (WDK) 8 附带的 WinUSB 应用程序模板</p>
<div class="alert">注意
<strong></strong>：对于常时等量传输，使用带有 Windows 驱动程序工具包 (WDK) 8.1 的 Visual Studio 2013
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td>编程语言</td>
<td>C#、VB.NET、C++、JavaScript</td>
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
<th>关键场景</th>
<th>UWP 应用</th>
<th>Windows 桌面应用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>设备发现</td>
<td>使用 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration" data-raw-source="[&lt;strong&gt;Windows.Devices.Enumeration&lt;/strong&gt;](/uwp/api/Windows.Devices.Enumeration)">Windows.Devices.Enumeration</a> 命名空间获取 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice" data-raw-source="[&lt;strong&gt;UsbDevice&lt;/strong&gt;](/uwp/api/Windows.Devices.Usb.UsbDevice)">UsbDevice</a>。</td>
<td>使用 <a href="/windows-hardware/drivers/install/setupapi" data-raw-source="[SetupAPI](/windows-hardware/drivers/install/setupapi)">SetupAPI</a> 函数和 <a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize" data-raw-source="[&lt;strong&gt;WinUsb_Initialize&lt;/strong&gt;](/windows/desktop/api/winusb/nf-winusb-winusb_initialize)">WinUsb_Initialize</a> 获取 WINUSB_INTERFACE_HANDLE。</td>
</tr>
<tr class="even">
<td>USB 控制传输</td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbSetupPacket" data-raw-source="[&lt;strong&gt;UsbSetupPacket&lt;/strong&gt;](/uwp/api/Windows.Devices.Usb.UsbSetupPacket)">UsbSetupPacket</a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbControlRequestType" data-raw-source="[&lt;strong&gt;UsbControlRequestType&lt;/strong&gt;](/uwp/api/Windows.Devices.Usb.UsbControlRequestType)">UsbControlRequestType</a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlInTransferAsync_Windows_Devices_Usb_UsbSetupPacket_Windows_Storage_Streams_IBuffer_" data-raw-source="[&lt;strong&gt;UsbDevice.SendControlInTransferAsync&lt;/strong&gt;](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlInTransferAsync_Windows_Devices_Usb_UsbSetupPacket_Windows_Storage_Streams_IBuffer_)">UsbDevice.SendControlInTransferAsync</a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlOutTransferAsync_Windows_Devices_Usb_UsbSetupPacket_" data-raw-source="[&lt;strong&gt;UsbDevice.SendControlOutTransferAsync&lt;/strong&gt;](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlOutTransferAsync_Windows_Devices_Usb_UsbSetupPacket_)">UsbDevice.SendControlOutTransferAsync</a></p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/ns-winusb-_winusb_setup_packet" data-raw-source="[&lt;strong&gt;WINUSB_SETUP_PACKET&lt;/strong&gt;](/windows/desktop/api/winusb/ns-winusb-_winusb_setup_packet)">WINUSB_SETUP_PACKET</a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer" data-raw-source="[&lt;strong&gt;WinUsb_ControlTransfer&lt;/strong&gt;](/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer)">WinUsb_ControlTransfer</a></p></td>
</tr>
<tr class="odd">
<td>获取 USB 描述符</td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DeviceDescriptor" data-raw-source="[&lt;strong&gt;UsbDevice.DeviceDescriptor&lt;/strong&gt;](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DeviceDescriptor)">UsbDevice.DeviceDescriptor</a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors" data-raw-source="[&lt;strong&gt;UsbConfiguration.Descriptors&lt;/strong&gt;](/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors)">UsbConfiguration.Descriptors</a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_Descriptors" data-raw-source="[&lt;strong&gt;UsbInterface.Descriptors&lt;/strong&gt;](/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_Descriptors)">UsbInterface.Descriptors</a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbEndpointDescriptor" data-raw-source="[&lt;strong&gt;UsbEndpointDescriptor&lt;/strong&gt;](/uwp/api/Windows.Devices.Usb.UsbEndpointDescriptor)">UsbEndpointDescriptor</a></p></td>
<td><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor)">WinUsb_GetDescriptor</a></td>
</tr>
<tr class="even">
<td>发送 USB 批量传输</td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe" data-raw-source="[&lt;strong&gt;UsbBulkInPipe&lt;/strong&gt;](/uwp/api/Windows.Devices.Usb.UsbBulkInPipe)">UsbBulkInPipe</a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe" data-raw-source="[&lt;strong&gt;UsbBulkOutPipe&lt;/strong&gt;](/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe)">UsbBulkInPipe</a></p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe" data-raw-source="[&lt;strong&gt;WinUsb_ReadPipe&lt;/strong&gt;](/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)">WinUsb_ReadPipe</a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe" data-raw-source="[&lt;strong&gt;WinUsb_WritePipe&lt;/strong&gt;](/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)">WinUsb_ReadPipe</a></p></td>
</tr>
<tr class="odd">
<td>发送 USB 中断传输</td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe" data-raw-source="[&lt;strong&gt;UsbInterruptInPipe&lt;/strong&gt;](/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe)">UsbInterruptInPipe</a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe" data-raw-source="[&lt;strong&gt;UsbInterruptOutPipe&lt;/strong&gt;](/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe)">UsbInterruptOutPipe</a></p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe" data-raw-source="[&lt;strong&gt;WinUsb_ReadPipe&lt;/strong&gt;](/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)">WinUsb_ReadPipe</a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe" data-raw-source="[&lt;strong&gt;WinUsb_WritePipe&lt;/strong&gt;](/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)">WinUsb_ReadPipe</a></p></td>
</tr>
<tr class="even">
<td>发送 USB 常时等量传输</td>
<td>不支持。</td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipe" data-raw-source="[&lt;strong&gt;WinUsb_ReadIsochPipe&lt;/strong&gt;](/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipe)">WinUsb_ReadIsochPipe</a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap" data-raw-source="[&lt;strong&gt;WinUsb_ReadIsochPipeAsap&lt;/strong&gt;](/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap)">WinUsb_ReadIsochPipeAsap</a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe" data-raw-source="[&lt;strong&gt;WinUsb_WriteIsochPipe&lt;/strong&gt;](/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe)">WinUsb_WriteIsochPipe</a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap" data-raw-source="[&lt;strong&gt;WinUsb_WriteIsochPipeAsap&lt;/strong&gt;](/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap)">WinUsb_WriteIsochPipeAsap</a></p></td>
</tr>
<tr class="odd">
<td>关闭设备</td>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_Close" data-raw-source="[&lt;strong&gt;UsbDevice.Close&lt;/strong&gt;](/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_Close)">UsbDevice.Close</a></td>
<td><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free" data-raw-source="[&lt;strong&gt;WinUsb_Free&lt;/strong&gt;](/windows/desktop/api/winusb/nf-winusb-winusb_free)">WinUsb_Free</a></td>
</tr>
</tbody>
</table>



## <a name="documentation"></a>文档


| 文档     | UWP 应用                                                                     | Windows 桌面应用                                                                                           |
|-------------------|---------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| 编程指南 | [与 USB 设备通信，从开始到完成](talking-to-usb-devices-start-to-finish.md) | [如何通过 WinUSB Functions 访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md) |
| API 参考     | [**Windows.Devices.Usb**](/uwp/api/Windows.Devices.Usb)                              | [WinUSB 函数](using-winusb-api-to-communicate-with-a-usb-device.md)                                     |



## <a name="related-topics"></a>相关主题
[通用串行总线 (USB)](../index.yml)