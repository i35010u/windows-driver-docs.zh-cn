---
Description: 本部分中的本主题描述的类驱动程序、 常规客户端驱动程序和由 Microsoft 提供的父复合驱动程序。
title: Microsoft 提供的 USB 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 572b867501af1658d4ef7d89c5880743bdfefaf5
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350194"
---
# <a name="microsoft-provided-usb-drivers"></a>Microsoft 提供的 USB 驱动程序


本部分中的本主题描述的类驱动程序、 常规客户端驱动程序和由 Microsoft 提供的父复合驱动程序。

## <a name="microsoft-provided-usb-drivers-for-controllers-and-hubs"></a>控制器和集线器的 USB 驱动程序提供由 Microsoft 提供


Microsoft 提供了这些组的驱动程序：

-   为 USB 主控制器和中心。 有关详细信息，请参阅[USB 宿主端驱动程序在 Windows 中的](usb-3-0-driver-stack-architecture.md)。 你可以开发自定义主机控制器驱动程序的通信使用 USB 主控制器扩展 (UCX) 驱动程序。 有关详细信息，请参阅[开发的 Windows USB 驱动程序托管控制器](developing-windows-drivers-for-usb-host-controllers.md)。
-   用于处理的 USB 设备的常见函数逻辑。 有关详细信息，请参阅[USB 设备端驱动程序在 Windows 中的](usb-device-side-drivers-in-windows.md)。
-   有关支持类型 C 连接器。 有关详细信息，请参阅[USB 连接器管理器类扩展 (UcmCx)](https://msdn.microsoft.com/library/windows/hardware/mt188011)。

## <a name="other-microsoft-provided-usb-drivers"></a>其他 Microsoft 提供的 USB 驱动程序


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>设备安装程序类</th>
<th>Microsoft 提供的驱动程序和 INF</th>
<th>Windows 支持</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>USB</td>
<td><p>Usbccgp.sys</p>
<p>Usb.inf</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p>
<p>Windows Vista</p>
<p>Windows XP</p></td>
<td>Usbccgp.sys 是父驱动程序的复合设备，支持多个函数。 有关详细信息，请参阅<a href="usb-common-class-generic-parent-driver.md" data-raw-source="[USB Generic Parent Driver (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)">USB 通用父驱动程序 (Usbccgp.sys)</a>。</td>
</tr>
<tr class="even">
<td>生物识别</td>
<td><p>WudfUsbBID.dll</p>
<p>WudfUsbBIDAdvanced.inf</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p></td>
<td><p>Microsoft 通过提供 Windows 生物识别框架来支持 USB 生物识别设备 （指纹读取器）。 请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff536448" data-raw-source="[Windows Biometric Framework](https://msdn.microsoft.com/library/windows/hardware/ff536448)">Windows 生物识别框架</a>。</p></td>
</tr>
<tr class="odd">
<td>媒体传输协议的设备</td>
<td>Wpdusb.sys （已过时）</td>
<td><p>Windows Server 2008</p>
<p>Windows Vista</p>
<p>Windows Server 2003</p>
<p>Windows XP</p></td>
<td><div class="alert">
<strong>注意</strong><br/><p>从 Windows 7 开始，Microsoft 已替换 Windows Vista USB 驱动程序堆栈 (Wpdusb.sys) 的内核模式组件的 Windows 便携式设备 (WPD) 与泛型 Winusb.sys。</p>
</div>
<div>

</div>
<p>Microsoft 提供了 Wpdusb.sys 驱动程序管理支持媒体传输协议的便携设备。 请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff597864" data-raw-source="[WPD Design Guide](https://msdn.microsoft.com/library/windows/hardware/ff597864)">WPD 设计指南</a>。</p></td>
</tr>
<tr class="even">
<td>USBDevice</td>
<td><p>Winusb.sys</p>
<p>Winusb.inf</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p>
<p>Windows Vista</p>
<p>Windows XP Service Pack 2 (SP2)</p></td>
<td>Winusb.sys 可以用作 USB 设备的功能而不是实现一个驱动程序的驱动程序。 请参阅<a href="how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md" data-raw-source="[WinUSB](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)">WinUSB</a>。</td>
</tr>
</tbody>
</table>



## <a name="microsoft-provided-usb-device-class-drivers"></a>Microsoft 提供 USB 设备类的驱动程序


Microsoft 提供多个 USB 设备类批准的 USB 驱动程序-如果。 在 Windows 中包含这些驱动程序和其安装文件。 在提供了\\Windows\\System32\\DriverStore\\资料库文件夹。

查看，请[USB 设备类驱动程序包含在 Windows 中](supported-usb-classes.md)。

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB)](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[USB 驱动程序开发指南](usb-driver-development-guide.md)  



