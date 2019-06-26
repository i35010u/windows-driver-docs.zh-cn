---
Description: 本主题列出的标头和所需的编写的 Windows 驱动程序模型 (WDM) USB 客户端驱动程序库。
title: USB 客户端驱动程序所需的标头和库
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86ac904d1cff057d67412bb3e98f762da30ea49f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378339"
---
# <a name="headers-and-libraries-required-by-a-usb-client-driver"></a>USB 客户端驱动程序所需的标头和库


本主题列出的标头和所需的编写的 Windows 驱动程序模型 (WDM) USB 客户端驱动程序库。

若要查找特定设备驱动程序接口 (DDI) 的标头和库，请参阅中的引用页[USB 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/)。

## <a name="headers"></a>标头


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
<th>包括</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>hubbusif.h</td>
<td>Include\km</td>
<td></td>
<td>定义导出的 USB 端口驱动程序，也可通过 USB 集线器驱动程序使用的服务。</td>
</tr>
<tr class="even">
<td>usb.h</td>
<td>Include\shared</td>
<td></td>
<td>定义<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb" data-raw-source="[&lt;strong&gt;URB&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)"> <strong>URB</strong> </a> USB 请求块 (URBs) 的客户端驱动程序将请求发送到 USB 驱动程序堆栈所需的结构。</td>
</tr>
<tr class="odd">
<td>usb100.h</td>
<td>Include\shared</td>
<td></td>
<td>定义 USB 描述符，根据官方 USB 1.0 规范。</td>
</tr>
<tr class="even">
<td>usb200.h</td>
<td>Include\shared</td>
<td><p>usb100.h</p></td>
<td>定义 USB 描述符，根据官方的 USB 2.0 规范。</td>
</tr>
<tr class="odd">
<td>usbbusif.h</td>
<td>Include\km</td>
<td></td>
<td>定义为想要直接链接到端口驱动程序而不是直接向 Usbd.sys 链接的 USB 客户端驱动程序 (FDO) 定义的总线接口。</td>
</tr>
<tr class="even">
<td>usbdi.h</td>
<td>Include\shared</td>
<td><p>usb.h</p>
<p>usbioctl.h</p></td>
<td>定义用于格式化 URBs 对于特定类型的请求的帮助器宏。</td>
</tr>
<tr class="odd">
<td>usbdlib.h</td>
<td>Include\km</td>
<td></td>
<td>定义 DDIs USB 客户端驱动程序用于将请求发送到 USB 驱动程序堆栈。</td>
</tr>
<tr class="even">
<td>usbdrivr.h</td>
<td>Include\km</td>
<td><p>usb.h</p>
<p>usbdlib.h</p>
<p>usbioctl.h</p>
<p>usbbusif.h</p></td>
<td>定义 USB_KERNEL_IOCTL。</td>
</tr>
<tr class="odd">
<td>usbioctl.h</td>
<td>Include\shared</td>
<td><p>usbiodef.h</p>
<p>usb200.h</p></td>
<td>定义 IOCTL USB 驱动程序堆栈所支持的代码。 包括客户端驱动程序; 内核模式 IOCTL 代码应用程序的用户模式下 IOCTL 代码。</td>
</tr>
<tr class="even">
<td>usbiodef.h</td>
<td>Include\shared</td>
<td></td>
<td>定义接口和 WMI Guid。</td>
</tr>
<tr class="odd">
<td>usbkern.h</td>
<td>Include\km</td>
<td><p>usbioctl.h</p></td>
<td>已弃用。</td>
</tr>
<tr class="even">
<td>usbrpmif.h</td>
<td>Include\um</td>
<td><p>usb100.h</p>
<p>windef.h</p>
<p>winapifamily.h</p></td>
<td>定义应用程序若要执行的 USB 设备的驱动程序重定向操作注册自己的函数。</td>
</tr>
<tr class="odd">
<td>usbspec.h</td>
<td>Include\shared</td>
<td></td>
<td>定义根据官方 USB 规范的设备驱动程序接口。</td>
</tr>
<tr class="even">
<td>usbuser.h</td>
<td>Include\um</td>
<td></td>
<td>定义支持的 USB 端口驱动程序的用户模式下 IOCTL 代码。</td>
</tr>
<tr class="odd">
<td>winusb.h</td>
<td>Include\um</td>
<td><p>winapifamily.h</p>
<p>winusbio.h</p></td>
<td>定义<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb" data-raw-source="[WinUSB functions](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)">WinUSB 函数</a>公开的 Winusb.dll，想要将请求发送到 Winusb.sys USB 设备的功能驱动程序作为安装的应用程序使用它们。</td>
</tr>
<tr class="even">
<td>winusbio.h</td>
<td>Include\shared</td>
<td><p>winapifamily.h</p>
<p>usb.h</p></td>
<td>为定义标志<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb" data-raw-source="[WinUSB functions](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)">WinUSB 函数</a>。</td>
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
<th>Library</th>
<th>路径</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>usbd.lib</td>
<td><p>\Lib\win8\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\win7\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\winv6.3\km&lt;em&gt;&lt;arch&gt;</em></p></td>
<td>从 USB 驱动程序堆栈中获取信息和设置 URBs 格式的请求提供帮助器例程。</td>
</tr>
<tr class="even">
<td>usbrpm.lib</td>
<td><p>\Lib\win8\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\win7\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\winv6.3\km&lt;em&gt;&lt;arch&gt;</em></p></td>
<td>提供了应用程序要执行操作的一个由 Microsoft 提供的驱动程序替换为第三方 RPM 驱动程序的函数。</td>
</tr>
<tr class="odd">
<td>usbdex.lib</td>
<td><p>\Lib\win8\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\win7\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\winv6.3\km&lt;em&gt;&lt;arch&gt;</em></p></td>
<td>提供客户端驱动程序将请求发送到基础的 USB 驱动程序堆栈的帮助器例程。 获取加载并在生成时以静态方式链接到客户端驱动程序模块库。 调用这些例程的客户端驱动程序可以在 Windows Vista 和更高版本的 Windows 上运行。</td>
</tr>
<tr class="even">
<td>winusb.lib</td>
<td><p>\Lib\win8\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\win8\um&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\win7\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\win7\um&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\winv6.3\km&lt;em&gt;&lt;arch&gt;</em></p>
<p>\Lib\winv6.3\um&lt;em&gt;&lt;arch&gt;</em></p></td>
<td>提供用于用户模式下客户端驱动程序或应用程序与具有 Winusb.sys 作为其功能驱动程序加载的 USB 设备进行通信的函数。</td>
</tr>
</tbody>
</table>

 

## <a name="header-changes-in-windows8"></a>Windows 8 中的标头更改


从 Windows 8 的 Windows Driver Kit (WDK) 中，标头文件 usbspec.h 替换 USBProtocolDefs.h。

新的头文件、 usbspec.h，提供了定义，按照官方 USB 规范 DDIs 的协议定义。 标头文件包括 DDIs USB 3.0 规范。

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  
[Windows 驱动程序工具包中的头文件](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/header-files-in-the-windows-driver-kit)  
[USB 客户端驱动程序开发入门](getting-started-with-usb-client-driver-development.md)  



