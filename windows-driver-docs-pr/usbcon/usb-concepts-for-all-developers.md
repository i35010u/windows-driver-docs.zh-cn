---
Description: A Universal Serial Bus (USB) device defines its capabilities and features through configurations, interfaces, alternate settings, and endpoints.
title: 所有 USB 开发人员的概念
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8a91ceaf9fb8602e0c507f1541ebce1ef7e0624
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547063"
---
#  <a name="concepts-for-all-usb-developers"></a>所有 USB 开发人员的概念


通用串行总线 (USB) 设备定义其功能和通过配置、 接口、 替代设置和终结点的功能。 本主题提供了这些概念的高级概述。 有关详细信息，请参阅上的 USB 规范[通用串行总线文档]( https://go.microsoft.com/fwlink/p/?linkid=224892)。

## <a name="in-this-section"></a>本部分内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="usb-device-layout.md" data-raw-source="[USB device layout](usb-device-layout.md)">USB 设备布局</a></p></td>
<td><p>USB 设备定义其功能和通过配置、 接口、 替代设置和终结点的功能。 本主题提供了这些概念的高级概述。</p></td>
</tr>
<tr class="even">
<td><p><a href="standard-usb-descriptors.md" data-raw-source="[Standard USB descriptors](standard-usb-descriptors.md)">标准 USB 描述符</a></p></td>
<td><p>USB 设备提供了有关其自身在名为的数据结构中的信息<em>USB 描述符</em>。 本部分提供有关设备、 配置、 接口和终结点描述符和方法从 USB 设备中检索信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-endpoints-and-their-pipes.md" data-raw-source="[USB endpoints and their pipes](usb-endpoints-and-their-pipes.md)">USB 终结点和其管道</a></p></td>
<td><p>USB 设备都有用于数据传输到的终结点。 在主机端，终结点都是管道。 本主题区分这些两个词之间。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-faq--introductory-level.md" data-raw-source="[USB in Windows - FAQ](usb-faq--introductory-level.md)">USB 中 Windows-常见问题解答</a></p></td>
<td><p>本主题介绍了一些常见问题的驱动程序开发人员还不熟悉开发以及将 USB 设备和驱动程序与 Windows 操作系统集成。</p></td>
</tr>
</tbody>
</table>

 

## <a name="common-usb-scenarios"></a>**常见的 USB 方案**


**1-获取设备句柄**通信并使用检索到的处理或对象以将数据发送传输。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>客户端驱动程序</th>
<th>UWP 应用</th>
<th>Windows 桌面应用程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KMDF</strong>:<a href="https://msdn.microsoft.com/library/windows/hardware/hh439428" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateWithParameters&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439428)"><strong>WdfUsbTargetDeviceCreateWithParameters</strong></a></p>
<p><strong>UMDF</strong>:<a href="https://msdn.microsoft.com/library/windows/hardware/ff560362" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560362)"><strong>IWDFUsbTargetDevice</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/apps/dn263883" data-raw-source="[&lt;strong&gt;UsbDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn263883)"><strong>UsbDevice</strong></a></p>
<p><a href="how-to-connect-to-a-usb-device--uwp-app-.md" data-raw-source="[How to connect to a USB device (UWP app)](how-to-connect-to-a-usb-device--uwp-app-.md)">如何连接到 USB 设备 （UWP 应用）</a>。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540277" data-raw-source="[&lt;strong&gt;WinUsb_Initialize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540277)"><strong>WinUsb_Initialize</strong></a></p>
<p>请参阅<a href="how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md" data-raw-source="[Write a Windows desktop app based on the WinUSB template](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)">编写基于 WinUSB 模板的 Windows 桌面应用</a>。</p></td>
</tr>
</tbody>
</table>

 

**USB 描述符检索**以获取有关设备的配置、 接口、 其他设置和其终结点的信息。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>客户端驱动程序</th>
<th>UWP 应用</th>
<th>Windows 桌面应用程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KMDF</strong>:</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550090" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceGetDeviceDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550090)"><strong>WdfUsbTargetDeviceGetDeviceDescriptor</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550098" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceRetrieveConfigDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550098)"><strong>WdfUsbTargetDeviceRetrieveConfigDescriptor</strong></a></p>
<p><strong>UMDF</strong>:</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560374" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::RetrieveDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560374)"><strong>IWDFUsbTargetDevice::RetrieveDescriptor</strong></a></p>
<p>请参阅<a href="usb-descriptors.md" data-raw-source="[USB descriptors](usb-descriptors.md)">USB 描述符</a>。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/apps/dn264002" data-raw-source="[&lt;strong&gt;UsbDevice.DeviceDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264002)"><strong>UsbDevice.DeviceDescriptor</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/apps/dn263802" data-raw-source="[&lt;strong&gt;UsbConfiguration.Descriptors&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn263802)"><strong>UsbConfiguration.Descriptors</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/apps/dn264289" data-raw-source="[&lt;strong&gt;UsbInterface.Descriptors&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264289)"><strong>UsbInterface.Descriptors</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/apps/dn264281" data-raw-source="[&lt;strong&gt;UsbInterfaceSetting.Descriptors&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264281)"><strong>UsbInterfaceSetting.Descriptors</strong></a></p>
<p><a href="how-to-get-usb-descriptors--uwp-app-.md" data-raw-source="[How to get USB descriptors (UWP app)](how-to-get-usb-descriptors--uwp-app-.md)">如何获取 USB 描述符 （UWP 应用）</a>。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540257" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540257)"><strong>WinUsb_GetDescriptor</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540292" data-raw-source="[&lt;strong&gt;WinUsb_QueryInterfaceSettings&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540292)"><strong>WinUsb_QueryInterfaceSettings</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540293" data-raw-source="[&lt;strong&gt;WinUsb_QueryPipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540293)"><strong>WinUsb_QueryPipe</strong></a></p>
<p>请参阅<a href="using-winusb-api-to-communicate-with-a-usb-device.md#query" data-raw-source="[Query the Device for USB Descriptors](using-winusb-api-to-communicate-with-a-usb-device.md#query)">USB 描述符查询设备</a>。</p></td>
</tr>
</tbody>
</table>

 

**2-配置设备**选择活动 USB 配置和设置每个接口。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>客户端驱动程序</th>
<th>UWP 应用</th>
<th>Windows 桌面应用程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KMDF:</strong></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550101" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSelectConfig&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550101)"><strong>WdfUsbTargetDeviceSelectConfig</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439423" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateUrb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439423)"><strong>WdfUsbTargetDeviceCreateUrb</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/hh406243" data-raw-source="[&lt;strong&gt;USBD_SelectConfigUrbAllocateAndBuild&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406243)"><strong>USBD_SelectConfigUrbAllocateAndBuild</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550073" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceSelectSetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550073)"><strong>WdfUsbInterfaceSelectSetting</strong></a></p>
<p>请参阅<a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">如何为 USB 设备选择一个配置</a>。</p>
<p>请参阅<a href="select-a-usb-alternate-setting.md" data-raw-source="[How to select an alternate setting in a USB interface](select-a-usb-alternate-setting.md)">如何在 USB 界面中选择一项备用设置</a>。</p>
<p><strong>UMDF:</strong></p>
<p>不支持配置所选内容。</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560343" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::SelectSetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560343)"><strong>IWDFUsbInterface::SelectSetting</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/apps/dn264286" data-raw-source="[&lt;strong&gt;UsbInterfaceSetting.SelectSettingAsync&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264286)"><strong>UsbInterfaceSetting.SelectSettingAsync</strong></a></p>
<p><a href="how-to-select-a-usb-interface-setting--uwp-app-.md" data-raw-source="[How to select a USB interface setting (UWP app)](how-to-select-a-usb-interface-setting--uwp-app-.md)">如何选择 USB 接口设置 （UWP 应用）</a>。</p></td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff540302" data-raw-source="[&lt;strong&gt;WinUsb_SetCurrentAlternateSetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540302)"><strong>WinUsb_SetCurrentAlternateSetting</strong></a></td>
</tr>
</tbody>
</table>

 

**3-发送的控制转移**配置设备并执行特定于特定设备的供应商命令。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>客户端驱动程序</th>
<th>UWP 应用</th>
<th>Windows 桌面应用程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KMDF:</strong></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550104" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550104)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550082" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550082)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/hh406243" data-raw-source="[&lt;strong&gt;USBD_SelectConfigUrbAllocateAndBuild&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406243)"><strong>USBD_SelectConfigUrbAllocateAndBuild</strong></a></p>
<p><strong>UMDF:</strong></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560363" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560363)"><strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong></a></p>
<p>请参阅<a href="usb-control-transfer.md" data-raw-source="[How to send a USB control transfer](usb-control-transfer.md)">如何发送 USB 控制传输</a>。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/apps/dn264037" data-raw-source="[&lt;strong&gt;SendControlInTransferAsync&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264037)"><strong>SendControlInTransferAsync</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/apps/dn264047" data-raw-source="[&lt;strong&gt;SendControlOutTransferAsync&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264047)"><strong>SendControlOutTransferAsync</strong></a></p>
<p><a href="how-to-send-a-usb-control-transfer--uwp-app-.md" data-raw-source="[How to send a USB control transfer (UWP app)](how-to-send-a-usb-control-transfer--uwp-app-.md)">如何发送 USB 控制传输 （UWP 应用）</a>。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540219" data-raw-source="[&lt;strong&gt;WinUsb_ControlTransfer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540219)"><strong>WinUsb_ControlTransfer</strong></a></p>
<p>请参阅<a href="using-winusb-api-to-communicate-with-a-usb-device.md#control" data-raw-source="[Send Control Transfer to the Default Endpoint](using-winusb-api-to-communicate-with-a-usb-device.md#control)">将控制传输发送到默认终结点</a>。</p></td>
</tr>
</tbody>
</table>

 

**4-发送大容量传输**，则通常由传输大量数据的大容量存储设备。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>客户端驱动程序</th>
<th>UWP 应用</th>
<th>Windows 桌面应用程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KMDF:</strong></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551155" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeReadSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551155)"><strong>WdfUsbTargetPipeReadSynchronously</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551163" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeWriteSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551163)"><strong>WdfUsbTargetPipeWriteSynchronously</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551136" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeFormatRequestForRead&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551136)"><strong>WdfUsbTargetPipeFormatRequestForRead</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551141" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeFormatRequestForWrite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551141)"><strong>WdfUsbTargetPipeFormatRequestForWrite</strong></a></p>
<p><a href="usb-bulk-and-interrupt-transfer.md" data-raw-source="[How to send USB bulk transfer requests](usb-bulk-and-interrupt-transfer.md)">如何发送 USB 大容量传输请求</a></p>
<p><a href="how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md" data-raw-source="[How to use the continuous reader for reading data from a USB pipe](how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md)">如何使用来从 USB 管道读取数据的连续读取器</a>。</p>
<p><strong>UMDF:</strong></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556908" data-raw-source="[&lt;strong&gt;IUsbTargetPipeContinuousReaderCallbackReadComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556908)"><strong>IUsbTargetPipeContinuousReaderCallbackReadComplete</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560391" data-raw-source="[&lt;strong&gt;IWDFUsbTargetPipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560391)"><strong>IWDFUsbTargetPipe</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560394" data-raw-source="[&lt;strong&gt;IWDFUsbTargetPipe2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560394)"><strong>IWDFUsbTargetPipe2</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/apps/dn297601" data-raw-source="[&lt;strong&gt;UsbBulkInPipe.InputStream&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn297601)"><strong>UsbBulkInPipe.InputStream</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/apps/dn297669" data-raw-source="[&lt;strong&gt;UsbBulkOutPipe.OutputStream&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn297669)"><strong>UsbBulkOutPipe.OutputStream</strong></a></p>
<p><a href="how-to-send-a-usb-bulk-transfer--uwp-app-.md" data-raw-source="[How to send a USB bulk transfer request (UWP app)](how-to-send-a-usb-bulk-transfer--uwp-app-.md)">如何将发送的 USB 大容量传输请求 （UWP 应用）</a>。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540322" data-raw-source="[&lt;strong&gt;WinUsb_WritePipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540322)"><strong>WinUsb_WritePipe</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540297" data-raw-source="[&lt;strong&gt;WinUsb_ReadPipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540297)"><strong>WinUsb_ReadPipe</strong></a></p>
<p>请参阅<a href="using-winusb-api-to-communicate-with-a-usb-device.md#io" data-raw-source="[Issue I/O Requests](using-winusb-api-to-communicate-with-a-usb-device.md#io)">发出 I/O 请求</a>。</p></td>
</tr>
</tbody>
</table>

 

**5-发送中断传输**。 若要检索的硬件中断数据中读取数据。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>客户端驱动程序</th>
<th>UWP 应用</th>
<th>Windows 桌面应用程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>大容量传输相同。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/apps/dn278418" data-raw-source="[&lt;strong&gt;UsbInterruptInPipe.DataReceived&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278418)"><strong>UsbInterruptInPipe.DataReceived</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/apps/dn278428" data-raw-source="[&lt;strong&gt;UsbInterruptOutPipe.OutputStream&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278428)"><strong>UsbInterruptOutPipe.OutputStream</strong></a></p>
<p><a href="how-to-send-a-usb-interrupt-transfer--uwp-app-.md" data-raw-source="[How to send a USB interrupt transfer request (UWP app)](how-to-send-a-usb-interrupt-transfer--uwp-app-.md)">如何发送 USB 中断传输请求 （UWP 应用）</a>。</p></td>
<td><p>大容量传输相同。</p></td>
</tr>
</tbody>
</table>

 

**6-发送同步传输**，主要用于媒体流式处理的设备。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>客户端驱动程序</th>
<th>UWP 应用</th>
<th>Windows 桌面应用程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KMDF:</strong></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439420" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateIsochUrb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439420)"><strong>WdfUsbTargetDeviceCreateIsochUrb</strong></a></p>
<p>请参阅<a href="transfer-data-to-isochronous-endpoints.md" data-raw-source="[How to transfer data to USB isochronous endpoints](transfer-data-to-isochronous-endpoints.md)">如何将数据传输到 USB 等时终结点</a>。</p>
<p><strong>UMDF:</strong>不支持。</p></td>
<td><p>不支持。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265566" data-raw-source="[&lt;strong&gt;WinUsb_RegisterIsochBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265566)"><strong>WinUsb_RegisterIsochBuffer</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265567" data-raw-source="[&lt;strong&gt;WinUsb_UnregisterIsochBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265567)"><strong>WinUsb_UnregisterIsochBuffer</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265569" data-raw-source="[&lt;strong&gt;WinUsb_WriteIsochPipeAsap&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265569)"><strong>WinUsb_WriteIsochPipeAsap</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265565" data-raw-source="[&lt;strong&gt;WinUsb_ReadIsochPipeAsap&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265565)"><strong>WinUsb_ReadIsochPipeAsap</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265568" data-raw-source="[&lt;strong&gt;WinUsb_WriteIsochPipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265568)"><strong>WinUsb_WriteIsochPipe</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265564" data-raw-source="[&lt;strong&gt;WinUsb_ReadIsochPipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265564)"><strong>WinUsb_ReadIsochPipe</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265549" data-raw-source="[&lt;strong&gt;WinUsb_GetCurrentFrameNumber&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265549)"><strong>WinUsb_GetCurrentFrameNumber</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265548" data-raw-source="[&lt;strong&gt;WinUsb_GetAdjustedFrameNumber&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265548)"><strong>WinUsb_GetAdjustedFrameNumber</strong></a></p>
<p>请参阅<a href="getting-set-up-to-use-windows-devices-usb.md" data-raw-source="[Sending USB isochronous transfers from a WinUSB desktop app](getting-set-up-to-use-windows-devices-usb.md)">从 WinUSB 桌面应用发送 USB 同步传输</a>。</p></td>
</tr>
</tbody>
</table>

 

**7-USB 选择性挂起**以允许设备进入低功耗状态，并将设备恢复到工作状态。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>客户端驱动程序</th>
<th>UWP 应用</th>
<th>Windows 桌面应用程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KMDF:</strong></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551270" data-raw-source="[&lt;strong&gt;WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551270)"><strong>WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545903" data-raw-source="[&lt;strong&gt;WdfDeviceAssignS0IdleSettings&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545903)"><strong>WdfDeviceAssignS0IdleSettings</strong></a></p>
<p><strong>UMDF:</strong></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560385" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::SetPowerPolicy&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560385)"><strong>IWDFUsbTargetDevice::SetPowerPolicy</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556920" data-raw-source="[&lt;strong&gt;IWDFDevice2::AssignS0IdleSettings&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556920)"><strong>IWDFDevice2::AssignS0IdleSettings</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/hh451202" data-raw-source="[&lt;strong&gt;IWDFDevice3::AssignS0IdleSettingsEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451202)"><strong>IWDFDevice3::AssignS0IdleSettingsEx</strong></a></p>
<p>请参阅<a href="https://msdn.microsoft.com/windows/hardware/gg463309" data-raw-source="[How to send a device to selective suspend](https://msdn.microsoft.com/windows/hardware/gg463309)">如何将发送设备到选择性挂起</a>。</p></td>
<td><p>不支持。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540309" data-raw-source="[&lt;strong&gt;WinUsb_SetPowerPolicy&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540309)"><strong>WinUsb_SetPowerPolicy</strong></a></p>
<p>请参阅<a href="winusb-power-management.md" data-raw-source="[WinUSB Power Management](winusb-power-management.md)">WinUSB 电源管理</a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB)](https://msdn.microsoft.com/library/windows/hardware/ff538930)  



