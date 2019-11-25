---
Description: 本主题提供了一些指导原则，用于确定是否应该编写 UWP 应用或 Windows 桌面应用以与 USB 设备通信。
title: 为 USB 设备开发 Windows 应用程序的概述
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 88e3dcae013cfc9d644ee8507ed77149c6b80e28
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007544"
---
# <a name="overview-of-developing-windows-applications-for-usb-devices"></a>为 USB 设备开发 Windows 应用程序的概述


**摘要**

-   选择正确编程模型的准则
-   UWP 应用和桌面应用开发人员体验

**重要的 API**

-   [**Windows.Devices.Usb**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)
-   [WinUSB 函数](using-winusb-api-to-communicate-with-a-usb-device.md)

本主题提供了一些指导原则，用于确定是否应该编写 UWP 应用或 Windows 桌面应用以与 USB 设备通信。

Windows 提供了 API 集，可用于编写与自定义 USB 设备通信的应用。 API 执行与 USB 相关的常见任务，例如查找设备和数据传输。

此环境中的 "自定义设备" 指的是 Microsoft 不提供内置类驱动程序的设备。 您可以改为安装 WinUSB （Winusb）作为设备驱动程序。

## <a name="choosing-a-programming-model"></a>选择编程模型


如果安装[Winusb](winusb-installation.md)，以下是编程模型选项：

-   [USB 设备的 UWP 应用](writing-usb-device-companion-apps-for-microsoft-store.md)

    Windows 8.1 提供新的命名空间：[**Windows. Usb**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)。 命名空间不能在早期版本的 Windows 中使用。 其他 Microsoft Store 资源如下所示：[UWP 应用](https://msdn.microsoft.com/windows/apps)。

-   [适用于 USB 设备的 Windows 桌面应用](windows-desktop-app-for-a-usb-device.md)

    在 Windows 8.1 之前，通过[Winusb](winusb-installation.md)进行通信的应用是使用[Winusb 函数](using-winusb-api-to-communicate-with-a-usb-device.md)编写的桌面应用。 在 Windows 8.1 中，已扩展了 API 集。 其他 Windows 桌面应用程序资源位于此处：[Windows 桌面应用程序](https://developer.microsoft.com/windows/desktop)。

选择最佳编程模型的策略取决于各种因素。

-   **应用是否会与内部 USB 设备通信？**

    Api 主要用于访问外围设备。 该 API 还可以访问 PC 内部 USB 设备。 但是，从 UWP 应用访问 PC 内部 USB 设备的权限限制为该电脑的 OEM 在设备元数据中显式声明的特权应用。

-   **应用是否会与 USB 同步终结点通信？**

    如果你的应用程序将数据传输到设备的同步终结点，则必须编写 Windows 桌面应用程序。 在 Windows 8.1 中，已将新的[WinUSB 函数](using-winusb-api-to-communicate-with-a-usb-device.md)添加到 API 集，使桌面应用能够将数据发送到同步终结点并从中接收数据。

-   **应用是否为 "控制面板" 类型的应用？**

    UWP 应用是每个用户的应用，不能在每个应用的范围之外进行更改。 对于这些类型的应用程序，必须编写 Windows 桌面应用程序。

-   **UWP 应用是否支持 USB 设备类？**

    如果设备属于这些设备类，请编写 UWP 应用。

    -   `name:cdcControl,           classId:02 * *`
    -   `name:physical, classId:05 * *`
    -   `name:personalHealthcare,   classId:0f 00 00`
    -   `name:activeSync,           classId:ef 01 01`
    -   `name:palmSync,             classId:ef 01 02`
    -   `name:deviceFirmwareUpdate, classId:fe 01 01`
    -   `name:irda,                 classId:fe 02 00     `
    -   `name:measurement,          classId:fe 03 *`
    -   `name:vendorSpecific,       classId:ff * *`

    **注意** 如果设备属于 DeviceFirmwareUpdate 类，则应用必须是特权应用。




如果设备不属于前面的设备类，请编写 Windows 桌面应用程序。


## <a name="driver-requirement"></a>驱动程序要求


| 驱动程序要求 | UWP 应用                                                                                                                          | Windows 桌面应用                                                                                                                       |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| 函数驱动程序    | Microsoft 提供的[Winusb](winusb-installation.md) （内核模式驱动程序）。                                                             | Microsoft 提供的[Winusb](winusb-installation.md) （内核模式驱动程序）。                                                            |
| 筛选器驱动程序      | 如果存在筛选器驱动程序，则仅限特权应用的访问权限。 此应用被 OEM 声明为设备元数据中的特权应用。 | 筛选器驱动程序可以出现在内核模式设备堆栈中，只要它不会阻止对[Winusb](winusb-installation.md)的访问。 |



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
<td>这些示例入门</td>
<td><ul>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[Custom USB device access sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">自定义 USB 设备访问示例</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[USB CDC Control sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">USB CDC 控制示例</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[Firmware Update USB Device sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">固件更新 USB 设备示例</a></li>
</ul></td>
<td><ul>
<li>从 Microsoft Visual Studio 附带的<strong>WinUsb 应用程序</strong>模板开始（旗舰版或专业版）</li>
<li>使用<a href="using-winusb-api-to-communicate-with-a-usb-device.md" data-raw-source="[How to Access a USB Device by Using WinUSB Functions](using-winusb-api-to-communicate-with-a-usb-device.md)">如何使用 WinUSB 函数访问 USB 设备</a>中所示的代码示例来扩展模板。</li>
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
<p>适用于 Windows 8.1 的 Microsoft Windows 软件开发工具包（SDK）</p></td>
<td><p>使用 Visual Studio （旗舰版或专业版）和 Windows 驱动程序工具包（WDK）8随附的<strong>WinUSB 应用程序</strong>模板</p>
<div class="alert">对于同步传输 
<strong>Note @ no__t，Visual Studio 2013 Windows 驱动程序工具包（WDK）8。1
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td>编程语言</td>
<td>C#，VB.NET， C++，JavaScript</td>
<td>ANSI-CC++</td>
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
<th>Windows 桌面应用</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>设备发现</td>
<td>使用<a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration" data-raw-source="[&lt;strong&gt;Windows.Devices.Enumeration&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration)"><strong>Windows.Devices.Enumeration</strong></a> <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice" data-raw-source="[&lt;strong&gt;UsbDevice&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice)">UsbDevice 命名空间获取一个。</td>
<td>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/install/setupapi" data-raw-source="[SetupAPI](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi)">setupapi.log</a>函数和<a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize" data-raw-source="[&lt;strong&gt;WinUsb_Initialize&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize)"><strong>WinUsb_Initialize</strong></a>获取 WINUSB_INTERFACE_HANDLE。</td>
</tr>
<tr class="even">
<td>USB 控件传输</td>
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
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors" data-raw-source="[&lt;strong&gt;UsbConfiguration.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors)"><strong>UsbConfiguration</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_Descriptors" data-raw-source="[&lt;strong&gt;UsbInterface.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_Descriptors)"><strong>UsbInterface</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbEndpointDescriptor" data-raw-source="[&lt;strong&gt;UsbEndpointDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbEndpointDescriptor)"><strong>UsbEndpointDescriptor</strong></a></p></td>
<td><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor)"><strong>WinUsb_GetDescriptor</strong></a></td>
</tr>
<tr class="even">
<td>正在发送 USB 批量传输</td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe" data-raw-source="[&lt;strong&gt;UsbBulkInPipe&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe)"><strong>UsbBulkInPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe" data-raw-source="[&lt;strong&gt;UsbBulkOutPipe&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe)"><strong>UsbBulkOutPipe</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe" data-raw-source="[&lt;strong&gt;WinUsb_ReadPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)"><strong>WinUsb_ReadPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe" data-raw-source="[&lt;strong&gt;WinUsb_WritePipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)"><strong>WinUsb_WritePipe</strong></a></p></td>
</tr>
<tr class="odd">
<td>正在发送 USB 中断传输</td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe" data-raw-source="[&lt;strong&gt;UsbInterruptInPipe&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe)"><strong>UsbInterruptInPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe" data-raw-source="[&lt;strong&gt;UsbInterruptOutPipe&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe)"><strong>UsbInterruptOutPipe</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe" data-raw-source="[&lt;strong&gt;WinUsb_ReadPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)"><strong>WinUsb_ReadPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe" data-raw-source="[&lt;strong&gt;WinUsb_WritePipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)"><strong>WinUsb_WritePipe</strong></a></p></td>
</tr>
<tr class="even">
<td>正在发送 USB 同步传输</td>
<td>不受支持。</td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipe" data-raw-source="[&lt;strong&gt;WinUsb_ReadIsochPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipe)"><strong>WinUsb_ReadIsochPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap" data-raw-source="[&lt;strong&gt;WinUsb_ReadIsochPipeAsap&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap)"><strong>WinUsb_ReadIsochPipeAsap</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe" data-raw-source="[&lt;strong&gt;WinUsb_WriteIsochPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe)"><strong>WinUsb_WriteIsochPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap" data-raw-source="[&lt;strong&gt;WinUsb_WriteIsochPipeAsap&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap)"><strong>WinUsb_WriteIsochPipeAsap</strong></a></p></td>
</tr>
<tr class="odd">
<td>关闭设备</td>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_Close" data-raw-source="[&lt;strong&gt;UsbDevice.Close&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_Close)"><strong>UsbDevice 关闭</strong></a></td>
<td><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free" data-raw-source="[&lt;strong&gt;WinUsb_Free&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free)"><strong>WinUsb_Free</strong></a></td>
</tr>
</tbody>
</table>



## <a name="documentation"></a>文档


| 文档     | UWP 应用                                                                     | Windows 桌面应用                                                                                           |
|-------------------|---------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| 编程指南 | [与 USB 设备通信，开始完成](talking-to-usb-devices-start-to-finish.md) | [如何使用 WinUSB 功能访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md) |
| API 参考     | [**Windows.Devices.Usb**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)                              | [WinUSB 函数](using-winusb-api-to-communicate-with-a-usb-device.md)                                     |



## <a name="related-topics"></a>相关主题
[通用串行总线 (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  



