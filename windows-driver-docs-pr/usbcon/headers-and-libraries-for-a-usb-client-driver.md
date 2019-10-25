---
Description: 本主题列出了写入 Windows 驱动模型（WDM） USB 客户端驱动程序所需的标头和库。
title: USB 客户端驱动程序所需的标头和库
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ce12d6cdfd4b3f3862f6f352a869694c41b8333
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844998"
---
# <a name="headers-and-libraries-required-by-a-usb-client-driver"></a>USB 客户端驱动程序所需的标头和库


本主题列出了写入 Windows 驱动模型（WDM） USB 客户端驱动程序所需的标头和库。

若要查找特定设备驱动程序接口（DDI）的标头和库，请参阅[USB 参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/)中的参考页。

## <a name="headers"></a>标题


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>标头文件</th>
<th>路径</th>
<th>涵盖</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>hubbusif</td>
<td>Include\km</td>
<td></td>
<td>定义 USB 端口驱动程序导出的、可供 USB 集线器驱动程序使用的服务。</td>
</tr>
<tr class="even">
<td>usb。h</td>
<td>Include\shared</td>
<td></td>
<td>为客户端驱动程序向 USB 驱动程序堆栈发送请求所需的 USB 请求块（URBs）定义<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)"><strong>URB</strong></a>结构。</td>
</tr>
<tr class="odd">
<td>usb100</td>
<td>Include\shared</td>
<td></td>
<td>根据官方 USB 1.0 规范定义 USB 描述符。</td>
</tr>
<tr class="even">
<td>usb200</td>
<td>Include\shared</td>
<td><p>usb100</p></td>
<td>根据官方 USB 2.0 规范定义 USB 描述符。</td>
</tr>
<tr class="odd">
<td>usbbusif</td>
<td>Include\km</td>
<td></td>
<td>定义为需要直接链接到端口驱动程序（而不是直接链接到 Usbd）的 USB 客户端驱动程序（FDO）定义的总线接口。</td>
</tr>
<tr class="even">
<td>usbdi</td>
<td>Include\shared</td>
<td><p>usb。h</p>
<p>usbioctl</p></td>
<td>定义用于对特定类型的请求进行格式设置的帮助器宏 URBs。</td>
</tr>
<tr class="odd">
<td>usbdlib</td>
<td>Include\km</td>
<td></td>
<td>定义 USB 客户端驱动程序用来向 USB 驱动程序堆栈发送请求的 DDIs。</td>
</tr>
<tr class="even">
<td>usbdrivr</td>
<td>Include\km</td>
<td><p>usb。h</p>
<p>usbdlib</p>
<p>usbioctl</p>
<p>usbbusif</p></td>
<td>定义 USB_KERNEL_IOCTL。</td>
</tr>
<tr class="odd">
<td>usbioctl</td>
<td>Include\shared</td>
<td><p>usbiodef</p>
<p>usb200</p></td>
<td>定义 USB 驱动程序堆栈支持的 IOCTL 代码。 包括客户端驱动程序的内核模式 IOCTL 代码;应用程序的用户模式 IOCTL 代码。</td>
</tr>
<tr class="even">
<td>usbiodef</td>
<td>Include\shared</td>
<td></td>
<td>定义接口和 WMI Guid。</td>
</tr>
<tr class="odd">
<td>usbkern</td>
<td>Include\km</td>
<td><p>usbioctl</p></td>
<td>已弃用。</td>
</tr>
<tr class="even">
<td>usbrpmif</td>
<td>Include\um</td>
<td><p>usb100</p>
<p>windef</p>
<p>winapifamily</p></td>
<td>定义一个应用程序的功能，以便为 USB 设备执行驱动程序重定向操作。</td>
</tr>
<tr class="odd">
<td>usbspec</td>
<td>Include\shared</td>
<td></td>
<td>根据官方 USB 规范定义设备驱动程序接口。</td>
</tr>
<tr class="even">
<td>usbuser</td>
<td>Include\um</td>
<td></td>
<td>定义 USB 端口驱动程序所支持的用户模式 IOCTL 代码。</td>
</tr>
<tr class="odd">
<td>winusb</td>
<td>Include\um</td>
<td><p>winapifamily</p>
<p>winusbio</p></td>
<td>定义由 Winusb 公开的<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb" data-raw-source="[WinUSB functions](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)">WinUSB 函数</a>，应用程序使用该函数将请求发送到安装为 USB 设备的函数驱动程序的 WinUSB。</td>
</tr>
<tr class="even">
<td>winusbio</td>
<td>Include\shared</td>
<td><p>winapifamily</p>
<p>usb。h</p></td>
<td>定义<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb" data-raw-source="[WinUSB functions](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)">WinUSB 函数</a>的标志。</td>
</tr>
</tbody>
</table>

 

## <a name="libraries"></a>库


<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>库</th>
<th>路径</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>usbd</td>
<td><p>\Lib\win8\km&lt;em&gt;&gt;&lt;</em></p>
<p>\Lib\win7\km&lt;em&gt;&gt;&lt;</em></p>
<p>\Lib\winv6.3\km&lt;em&gt;&gt;&lt;</em></p></td>
<td>提供帮助程序例程，用于从 USB 驱动程序堆栈获取信息并为请求设置 URBs 格式。</td>
</tr>
<tr class="even">
<td>usbrpm</td>
<td><p>\Lib\win8\km&lt;em&gt;&gt;&lt;</em></p>
<p>\Lib\win7\km&lt;em&gt;&gt;&lt;</em></p>
<p>\Lib\winv6.3\km&lt;em&gt;&gt;&lt;</em></p></td>
<td>为应用程序提供用于执行将 Microsoft 提供的驱动程序替换为第三方 RPM 驱动程序的操作的函数。</td>
</tr>
<tr class="odd">
<td>usbdex</td>
<td><p>\Lib\win8\km&lt;em&gt;&gt;&lt;</em></p>
<p>\Lib\win7\km&lt;em&gt;&gt;&lt;</em></p>
<p>\Lib\winv6.3\km&lt;em&gt;&gt;&lt;</em></p></td>
<td>提供客户端驱动程序的帮助程序例程，用于向基础 USB 驱动程序堆栈发送请求。 生成库时，库将加载并静态链接到客户端驱动程序模块。 调用这些例程的客户端驱动程序可以在 Windows Vista 和更高版本的 Windows 上运行。</td>
</tr>
<tr class="even">
<td>winusb</td>
<td><p>\Lib\win8\km&lt;em&gt;&gt;&lt;</em></p>
<p>\Lib\win8\um&lt;em&gt;&gt;&lt;</em></p>
<p>\Lib\win7\km&lt;em&gt;&gt;&lt;</em></p>
<p>\Lib\win7\um&lt;em&gt;&gt;&lt;</em></p>
<p>\Lib\winv6.3\km&lt;em&gt;&gt;&lt;</em></p>
<p>\Lib\winv6.3\um&lt;em&gt;&gt;&lt;</em></p></td>
<td>为用户模式客户端驱动程序或应用程序提供用于与已加载 Winusb 作为其函数驱动程序的 USB 设备进行通信的函数。</td>
</tr>
</tbody>
</table>

 

## <a name="header-changes-in-windows8"></a>Windows 8 中的标头更改


从适用于 Windows 8 的 Windows 驱动程序工具包（WDK）开始，标头文件 usbspec 将替换 USBProtocolDefs。

新标头文件 usbspec 为定义的 DDIs 提供协议定义，这是根据正式的 USB 规范提供的。 标头文件包括用于 USB 3.0 规格的 DDIs。

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  
[Windows 驱动程序工具包中的头文件](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/header-files-in-the-windows-driver-kit)  
[USB 客户端驱动程序开发入门](getting-started-with-usb-client-driver-development.md)  



