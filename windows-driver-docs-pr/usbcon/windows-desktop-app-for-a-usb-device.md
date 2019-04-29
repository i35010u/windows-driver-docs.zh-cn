---
Description: 了解如何应用程序可以调用 WinUSB 函数与 USB 设备进行通信。
title: USB 设备的 Windows 桌面应用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 557ae71709675dc25facc322c8d9a752fbd2c73f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389188"
---
# <a name="windows-desktop-app-for-a-usb-device"></a>USB 设备的 Windows 桌面应用


将本主题中了解有关应用程序可以调用[WinUSB 函数](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)与 USB 设备进行通信。 有关此类应用程序[WinUSB](winusb.md) (Winusb.sys) 必须作为设备的功能驱动程序安装。 在设备的内核模式堆栈 WinUSB。 此驱动程序包含在 Windows 中\\Windows\\System32\\驱动程序文件夹。

如果使用的 Winusb.sys 作为 USB 设备的功能驱动程序，则可以调用[WinUSB 函数](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)从应用程序以与设备通信。 这些函数中，公开的用户模式 DLL Winusb.dll，简化通信过程。 而不是构造设备 I/O 控制请求以执行标准 USB 操作 （如配置设备、 发送控制请求以及将数据传输到或从设备），应用程序调用等效 WinUSB 函数。

Winusb.dll 使用的应用程序提供的数据来构造相应的设备的 I/O 控制请求，然后将请求发送到 Winusb.sys 进行处理。 若要与 USB 堆栈进行通信，WinUSB 函数调用[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)与相应 IOCTL 的与应用程序的请求相关联的函数。 请求完成后，WinUSB 函数将传递回调用进程 （如来自的读取请求的数据） 的 Winusb.sys 返回任何信息。 如果在调用**DeviceIoControl**是成功，它将返回一个非零值。 如果调用失败或被挂起 （不立即处理）， **DeviceIoControl**返回零值。 如果出现错误，应用程序可以调用[ **GetLastError** ](https://msdn.microsoft.com/library/windows/desktop/ms679360)的更详细的错误消息。

更为简单使用 WinUSB 函数不是它是实现一个驱动程序与设备通信。 但请注意以下限制：

-   WinUSB 函数允许一个应用程序一次以与设备通信。 如果您需要多个应用程序与设备同时进行通信，则必须实现功能驱动程序。
-   在 Windows 8.1 之前 WinUSB 函数不支持流式处理数据传入或传出同步终结点。
-   WinUSB 函数不支持已有内核模式下支持的设备。 此类设备的示例包括调制解调器和网络适配器，分别由电话服务 API (TAPI) 和 NDIS，支持。
-   对于多功能设备，可以使用设备的 INF 文件单独为每个 USB 函数指定一个框中的内核模式驱动程序或 Winusb.sys。 但是，您可以指定特定的函数，不能同时为这些选项之一。

**请注意**  WinUSB 函数需要 Windows XP 或更高版本。 可以在 C 中使用这些函数 /C++应用程序与您的 USB 设备进行通信。 若要编写使用 WinUSB Api 的 UWP 应用，请参阅[USB 设备的 UWP 应用](writing-usb-device-companion-apps-for-microsoft-store.md)。

## <a name="getting-started"></a>入门...


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>步骤</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>步骤 1</strong>— 获取您需要编写一个 Windows 桌面应用，适用于设备的工具。</p></td>
<td><ul>
<li>安装<a href="https://go.microsoft.com/fwlink/p/?LinkId=623328" data-raw-source="[Microsoft Visual Studio (Ultimate or Professional)]( https://go.microsoft.com/fwlink/p/?LinkId=623328)">Microsoft Visual Studio （Ultimate 或 Professional）</a>。</li>
<li>安装<a href="http://download.microsoft.com/download/E/C/E/ECE11176-1E40-46E7-A24B-D507D7F6FB65/wdk/wdksetup.exe" data-raw-source="[Windows Driver Kit (WDK) 8.1](http://download.microsoft.com/download/E/C/E/ECE11176-1E40-46E7-A24B-D507D7F6FB65/wdk/wdksetup.exe)">Windows 驱动程序工具包 (WDK) 8.1</a>。</li>
</ul>
<div class="alert">
<strong>请注意</strong>  安装 WDK 8.1 之前必须安装 Visual Studio。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td><p><strong>步骤 2</strong>— 获取测试 USB 设备和其硬件规范。 使用规范来确定应用程序和相关的设计决策的功能。</p></td>
<td><p>为了方便学习，受欢迎的选项有：</p>
<ul>
<li>OSR USB FX2 学习工具包。 此工具包最适合学习本文档集中包括的 USB 示例。 就可以从学习工具包<a href="http://www.osronline.com/" data-raw-source="[OSR Online](http://www.osronline.com/)">OSR 联机</a>。</li>
<li>Microsoft USB 测试工具 (MUTT) 设备。 可以从购买 MUTT 硬件<a href="http://jjgtechnologies.com/mutt.md" data-raw-source="[JJG Technologies](http://jjgtechnologies.com/mutt.md)">JJG 技术</a>。 设备没有安装的已安装的固件。 若要安装固件，下载从 MUTT 软件包<a href="mutt-software-package.md" data-raw-source="[this Web site](mutt-software-package.md)">此网站</a>并运行 MUTTUtil.exe。 有关详细信息，请参阅随程序包提供的文档。</li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>步骤 3</strong>— 编写获取设备的句柄的主干应用。</p></td>
<td><p>可以在以下两种方式编写第一个应用：</p>
<ul>
<li><p>编写基于 WinUSB 模板包含在 Visual Studio 应用程序。 有关详细信息，请参阅<a href="how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md" data-raw-source="[Write a Windows desktop app based on the WinUSB template](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)">编写基于 WinUSB 模板的 Windows 桌面应用</a>。</p></li>
<li><p>调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff550855" data-raw-source="[SetupAPI](https://msdn.microsoft.com/library/windows/hardware/ff550855)">SetupAPI</a>例程，从而获取你的设备的句柄并将其打开通过调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff540277" data-raw-source="[&lt;strong&gt;WinUsb_Initialize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540277)"> <strong>WinUsb_Initialize</strong></a>。 有关详细信息，请参阅<a href="using-winusb-api-to-communicate-with-a-usb-device.md" data-raw-source="[How to Access a USB Device by Using WinUSB Functions](using-winusb-api-to-communicate-with-a-usb-device.md)">如何访问由使用 WinUSB 函数 USB 设备</a>。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>步骤 6</strong>— 安装 Winusb.sys 为你的设备。</p></td>
<td><p>安装 Winusb.sys 适用于你的设备。</p>
<ul>
<li>如果使用的 Visual Studio，可驱动程序包安装在目标计算机上，通过使用 Visual Studio 部署。 有关说明，请参阅<a href="how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md" data-raw-source="[Write a Windows desktop app based on the WinUSB template](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)">编写基于 WinUSB 模板的 Windows 桌面应用</a>。</li>
<li>否则，手动安装该驱动程序在设备管理器通过编写自定义 INF。 有关详细信息，请参阅<a href="winusb-installation.md" data-raw-source="[WinUSB (Winusb.sys) Installation](winusb-installation.md)">WinUSB (Winusb.sys) 安装</a>。</li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>步骤 4</strong>-获取有关你的设备的信息并查看其描述符。 有关概念性信息，请参阅<a href="usb-concepts-for-all-developers.md" data-raw-source="[Concepts for all USB developers](usb-concepts-for-all-developers.md)">的所有 USB 开发人员概念</a>。</p></td>
<td><p>通过阅读配置描述符，接口描述符的每个受支持的替代设置，并将其终结点描述符获取有关设备功能的信息。</p>
<p>有关信息，请参阅<a href="using-winusb-api-to-communicate-with-a-usb-device.md#query" data-raw-source="[Query the Device for USB Descriptors](using-winusb-api-to-communicate-with-a-usb-device.md#query)">USB 描述符查询设备</a>。</p></td>
</tr>
<tr class="even">
<td><strong>步骤 5</strong>-从应用发送的 USB 控制传输。</td>
<td><p>将标准控制请求和供应商命令发送到你的设备。 有关详细信息，请参阅<a href="using-winusb-api-to-communicate-with-a-usb-device.md#control" data-raw-source="[Send Control Transfer to the Default Endpoint](using-winusb-api-to-communicate-with-a-usb-device.md#control)">发送到默认终结点传输控件</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>步骤 6</strong>— 从您的应用程序传输发送大容量或中断。</p></td>
<td><p>执行读取和写入操作，在大容量、 中断和由你的设备支持同步终结点。 有关详细信息，请参阅<a href="using-winusb-api-to-communicate-with-a-usb-device.md#io" data-raw-source="[Issue I/O Requests](using-winusb-api-to-communicate-with-a-usb-device.md#io)">问题 I/O 请求</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>步骤 7</strong>-从应用发送同步传输。</p></td>
<td><p>发送同步读取和写入请求，主要用于流式处理数据。 此功能才可在 Windows 8.1 上。 有关详细信息，请参阅<a href="getting-set-up-to-use-windows-devices-usb.md" data-raw-source="[Sending USB isochronous transfers from a WinUSB desktop app](getting-set-up-to-use-windows-devices-usb.md)">从 WinUSB 桌面应用发送 USB 同步传输</a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[USB 设备的 Windows 应用程序开发](developing-windows-applications-that-communicate-with-a-usb-device.md)  
[通用串行总线 (USB)](https://msdn.microsoft.com/library/windows/hardware/ff538930)  



