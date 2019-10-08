---
Description: 本节中的主题介绍了 Microsoft 提供的类驱动程序、通用客户端驱动程序和父复合驱动程序。
title: Microsoft 提供的 USB 驱动程序的概述
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 689df8bf0f99b3f38a27bb1943a8bae61de86cfc
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007643"
---
# <a name="overview-of-microsoft-provided-usb-drivers"></a>Microsoft 提供的 USB 驱动程序的概述


本节中的主题介绍了 Microsoft 提供的类驱动程序、通用客户端驱动程序和父复合驱动程序。

## <a name="microsoft-provided-usb-drivers-for-controllers-and-hubs"></a>适用于控制器和集线器的 Microsoft 提供的 USB 驱动程序


Microsoft 提供了这些驱动程序集：

-   适用于 USB 主机控制器和集线器。 有关详细信息，请参阅[Windows 中的 USB 主机端驱动程序](usb-3-0-driver-stack-architecture.md)。 可以开发自定义主机控制器驱动程序，该驱动程序与 USB 主机控制器扩展（UCX）驱动程序通信。 有关详细信息，请参阅[开发适用于 USB 主机控制器的 Windows 驱动程序](developing-windows-drivers-for-usb-host-controllers.md)。
-   用于处理 USB 设备的公用功能逻辑。 有关详细信息，请参阅[Windows 中的 USB 设备端驱动程序](usb-device-side-drivers-in-windows.md)。
-   用于支持 C 类型的连接器。 有关详细信息，请参阅[USB 连接器管理器类扩展（UcmCx）](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188011(v=vs.85))。

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
<p>Usb .inf</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p>
<p>Windows Vista</p>
<p>Windows XP</p></td>
<td>Usbccgp 是支持多个函数的复合设备的父驱动程序。 有关详细信息，请参阅<a href="usb-common-class-generic-parent-driver.md" data-raw-source="[USB Generic Parent Driver (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)">USB 通用父驱动程序（Usbccgp）</a>。</td>
</tr>
<tr class="even">
<td>生物识别</td>
<td><p>WudfUsbBID</p>
<p>WudfUsbBIDAdvanced .inf</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p></td>
<td><p>Microsoft 通过提供 Windows Biometric Framework 来支持 USB 生物识别设备（指纹读取器）。 请参阅<a href="https://docs.microsoft.com/previous-versions/ff536448(v=vs.85)" data-raw-source="[Windows Biometric Framework](https://docs.microsoft.com/previous-versions/ff536448(v=vs.85))">Windows Biometric Framework</a>。</p></td>
</tr>
<tr class="odd">
<td>媒体传输协议设备</td>
<td>Wpdusb （已过时）</td>
<td><p>Windows Server 2008</p>
<p>Windows Vista</p>
<p>Windows Server 2003</p>
<p>Windows XP</p></td>
<td><div class="alert">
<strong>注意</strong><br/><p>从 Windows 7 开始，Microsoft 已将适用于 Windows 的 windows 便携设备（WPD）的内核模式组件替换为通用 Winusb。</p>
</div>
<div>

</div>
<p>Microsoft 提供 Wpdusb 驱动程序来管理支持媒体传输协议的便携设备。 请参阅<a href="https://docs.microsoft.com/previous-versions/ff597864(v=vs.85)" data-raw-source="[WPD Design Guide](https://docs.microsoft.com/previous-versions/ff597864(v=vs.85))">WPD 设计指南</a>。</p></td>
</tr>
<tr class="even">
<td>USBDevice</td>
<td><p>Winusb.sys</p>
<p>Winusb .inf</p></td>
<td><p>Windows 8.1</p>
<p>Windows 8</p>
<p>Windows 7</p>
<p>Windows Vista</p>
<p>带有 Service Pack 2 （SP2）的 Windows XP</p></td>
<td>Winusb 可用作 USB 设备的函数驱动程序，而不是实现驱动程序。 请参阅<a href="how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md" data-raw-source="[WinUSB](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)">WinUSB</a>。</td>
</tr>
</tbody>
</table>



## <a name="microsoft-provided-usb-device-class-drivers"></a>Microsoft 提供的 USB 设备类驱动程序


Microsoft 为 USB 提供批准的几个 USB 设备类提供驱动程序。 这些驱动程序及其安装文件包含在 Windows 中。 它们在 \\Windows @ no__t-1System32 @ no__t-2DriverStore @ no__t 文件夹中提供。

请参阅[Windows 附带的 USB 设备类驱动程序](supported-usb-classes.md)。

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  
[USB 驱动程序开发指南](usb-driver-development-guide.md)  



