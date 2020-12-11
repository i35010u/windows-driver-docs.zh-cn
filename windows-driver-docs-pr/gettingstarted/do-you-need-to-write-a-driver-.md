---
title: 是否需要编写驱动程序
description: Microsoft Windows 包含适用于许多设备类型的内置驱动程序。 如果有适用于你的设备类型的内置驱动程序，则不必自行编写驱动程序。 你的设备可以使用内置的驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0122ea131ba1041df3d11573ccd1875846961a41
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795533"
---
# <a name="do-you-need-to-write-a-driver"></a>是否需要编写驱动程序？


Microsoft Windows 包含适用于许多设备类型的内置驱动程序。 如果有适用于你的设备类型的内置驱动程序，则不必自行编写驱动程序。 你的设备可以使用内置的驱动程序。

## <a name="span-idbuilt-in_drivers_for_usb_devicesspanspan-idbuilt-in_drivers_for_usb_devicesspanspan-idbuilt-in_drivers_for_usb_devicesspanbuilt-in-drivers-for-usb-devices"></a><span id="Built-in_drivers_for_USB_devices"></span><span id="built-in_drivers_for_usb_devices"></span><span id="BUILT-IN_DRIVERS_FOR_USB_DEVICES"></span>适用于 USB 设备的内置驱动程序


如果你的设备属于由 USB 设备工作组 (DWG) 定义的设备类，则可能已经存在适用于该设备的 Windows USB 类驱动程序。 有关详细信息，请参阅[支持的 USB 设备类的驱动程序](/windows-hardware/drivers/ddi/index)。

## <a name="span-idbuilt-in_drivers_for_other_devicesspanspan-idbuilt-in_drivers_for_other_devicesspanspan-idbuilt-in_drivers_for_other_devicesspanbuilt-in-drivers-for-other-devices"></a><span id="Built-in_drivers_for_other_devices"></span><span id="built-in_drivers_for_other_devices"></span><span id="BUILT-IN_DRIVERS_FOR_OTHER_DEVICES"></span>适用于其他设备的内置驱动程序


目前，Microsoft 为以下其他类型的设备提供了内置驱动程序：

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">设备技术和驱动程序</th>
<th align="left">内置驱动程序</th>
<th align="left">Windows 支持</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ACPI：ACPI 驱动程序</p></td>
<td align="left"><p>Acpi.sys</p></td>
<td align="left"><p>Windows XP 及更高版本</p></td>
<td align="left"><p>Microsoft 通过 Acpi.sys 驱动程序和 ACPI BIOS 为基本的 ACPI 设备功能提供支持。 为增强 ACPI 设备的功能，供应商可以提供 WDM 功能驱动程序。 有关 Windows ACPI 支持的详细信息，请参阅 ACPI 设计指南中的<a href="/windows-hardware/drivers/acpi/supporting-acpi-devices" data-raw-source="[Supporting ACPI Devices](../acpi/supporting-acpi-devices.md)">支持 ACPI 设备</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>音频：Microsoft 音频类驱动程序</p></td>
<td align="left"><p>PortCls.sys</p></td>
<td align="left"><p>Windows XP 及更高版本</p></td>
<td align="left"><p>Microsoft 通过自身的端口类驱动程序 (PortCl) 为基本的音频渲染和音频捕捉提供支持。 音频设备的硬件供应商有责任提供兼容 PortCl 的适配器驱动程序。 适配器驱动程序包括初始化代码、驱动程序管理代码（包括 DriverEntry 功能）和音频微型端口驱动程序的集合。 有关详细信息，请参阅<a href="/windows-hardware/drivers/audio/introduction-to-port-class" data-raw-source="[Introduction to Port Class](../audio/introduction-to-port-class.md)">端口类简介</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>总线：本机 SD 总线驱动程序、本机 SD 存储类驱动程序和存储微型端口驱动程序</p></td>
<td align="left"><p>sdbus.sys、sffdisk.sys、sffp_sd.sys</p></td>
<td align="left"><p>Windows Vista 及更高版本</p></td>
<td align="left"><p>Microsoft 支持 SD 卡读卡器，如下所述：操作系统支持直接连接到 PCI 总线的 SD 主机控制器。 当系统枚举 SD 主机控制器时，会加载本机 SD 总线驱动程序 (sdbus.sys)。 如果用户插入 SD 内存卡，则除总线驱动程序以外，Windows 还会加载本机 SD 存储类驱动程序 (sffdisk.sys) 和存储微型端口驱动程序 (sffp_sd.sys)。 如果用户插入具有其他类型功能的 SD 卡（例如 GPS 或无线 LAN），则 Windows 会加载供应商为该设备提供的驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HID：HID I2C 驱动程序</p></td>
<td align="left"><p>HIDI2C.sys</p></td>
<td align="left"><p>Windows 8 及更高版本</p></td>
<td align="left"><p>Microsoft 为支持简单外设总线 (SPB) 和通用 I/O (GPIO) 的 SoC 系统上的 HID over I2C 设备提供支持。 它通过 HIDI2C.sys 驱动程序实现此支持。 有关详细信息，请参阅 <a href="/windows-hardware/drivers/hid/hid-over-i2c-guide" data-raw-source="[HID over I2C](../hid/hid-over-i2c-guide.md)">HID over I2C</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HID：传统游戏端口驱动程序</p></td>
<td align="left"><p>HidGame.sys、Gameenum.sys</p></td>
<td align="left"><p>Windows Vista</p>
<p>Windows Server 2003</p>
<p>Windows XP</p></td>
<td align="left"><p>在 Windows Vista 及更早版本中，Microsoft 通过 HidGame.sys 和 Gameenum.sys 驱动程序为传统（非 USB、非蓝牙、非 I2C）游戏端口提供支持。 有关详细信息，请参阅 <a href="/previous-versions/jj126201(v=vs.85)" data-raw-source="[HID Transports Supported in Windows](/previous-versions/jj126201(v=vs.85))">Windows 中支持的 HID 传输</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HID：传统键盘类驱动程序</p></td>
<td align="left"><p>Kbdclass.sys</p></td>
<td align="left"><p>Windows XP 及更高版本</p></td>
<td align="left"><p>Microsoft 通过 Kbdclass.sys 驱动程序为传统（非 USB、非蓝牙、非 I2C）键盘提供支持。 有关详细信息，请参阅键盘和鼠标 HID 客户端驱动程序。 为增强传统键盘的功能，供应商可以提供键盘筛选器驱动程序。 有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=618052" data-raw-source="[Kbfiltr sample](https://go.microsoft.com/fwlink/p/?LinkId=618052)">Kbfiltr 示例</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HID：传统鼠标类驱动程序</p></td>
<td align="left"><p>Mouclass.sys</p></td>
<td align="left"><p>Windows XP 及更高版本</p></td>
<td align="left"><p>Microsoft 通过 Mouclass.sys 驱动程序为传统（非 USB、非蓝牙、非 I2C）鼠标提供支持。 键盘和鼠标 HID 客户端驱动程序。 为增强传统鼠标的功能，供应商可以提供鼠标筛选器驱动程序。 有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=618052" data-raw-source="[Moufiltr sample](https://go.microsoft.com/fwlink/p/?LinkId=618052)">Moufiltr 示例</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HID：PS/2 (i8042prt) 驱动程序</p></td>
<td align="left"><p>I8042prt.sys</p></td>
<td align="left"><p>Windows XP 及更高版本</p></td>
<td align="left"><p>Microsoft 通过 I8042.sys 驱动程序为传统 PS/2 键盘和鼠标提供支持。 为增强 PS/2 鼠标或键盘的功能，供应商可以提供键盘或鼠标筛选器驱动程序。 有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=618052" data-raw-source="[Kbfiltr sample](https://go.microsoft.com/fwlink/p/?LinkId=618052)">Kbfiltr 示例</a>和 <a href="https://go.microsoft.com/fwlink/p/?LinkId=618052" data-raw-source="[Moufiltr sample](https://go.microsoft.com/fwlink/p/?LinkId=618052)">Moufiltr 示例</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>图像处理：设备的 Web 服务 (WSD) 扫描类驱动程序</p></td>
<td align="left"><p>WSDScan.sys</p></td>
<td align="left"><p>Windows Vista 及更高版本</p></td>
<td align="left"><p>Microsoft 通过 WSD 扫描驱动程序 (wsdscan.sys) 为 Web 服务扫描程序（即在 Web 上使用的扫描程序）提供支持。 但是，支持 WSD 分布式扫描管理的 Web 服务扫描程序设备必须实现两个 Web 服务协议。 有关详细信息，请参阅<a href="/windows-hardware/drivers/image/wia-with-web-services-for-devices" data-raw-source="[WIA with Web Services for Devices](../image/wia-with-web-services-for-devices.md)">使用设备 Web 服务的 WIA</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>打印：Microsoft 绘图仪驱动程序</p></td>
<td align="left"><p>Msplot</p></td>
<td align="left"><p>Windows XP 及更高版本</p></td>
<td align="left"><p>Microsoft 通过 Microsoft 绘图仪驱动程序 (Msplot) 为支持惠普图形语言的绘图仪提供支持。 为增强绘图仪的功能，你可以创建由一个或多个绘图仪特性数据 (PCD) 文件组成的微型驱动程序。 有关详细信息，请参阅<a href="/windows-hardware/drivers/print/plotter-driver-minidrivers" data-raw-source="[Plotter Driver Minidrivers](../print/plotter-driver-minidrivers.md)">绘图仪驱动程序微型驱动程序</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>打印：Microsoft PostScript 打印机驱动程序</p></td>
<td align="left"><p>Pscript</p></td>
<td align="left"><p>Windows XP 及更高版本</p></td>
<td align="left"><p>Microsoft 通过 PostScript 打印机驱动程序 (Pscript) 为 PostScript 打印机提供支持。 为增强 PostScript 打印机的功能，你可以创建由一个或多个 PostScript 打印机描述 (PPD) 文件和字体 (NTF) 文件组成的微型驱动程序。 有关详细信息，请参阅 <a href="/windows-hardware/drivers/print/pscript-minidrivers" data-raw-source="[Pscript Minidrivers](../print/pscript-minidrivers.md)">Pscript 微型驱动程序</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>打印：Microsoft 通用打印机驱动程序</p></td>
<td align="left"><p>Unidrv</p></td>
<td align="left"><p>Windows XP 及更高版本</p></td>
<td align="left"><p>Microsoft 通过通用打印机驱动程序 (Unidrv) 为非 PostScript 打印机提供支持。 为增强非 PostScript 打印机的功能，你可以创建由一个或多个通用打印机描述 (GPD) 文件组成的微型驱动程序。 有关详细信息，请参阅 <a href="/windows-hardware/drivers/print/microsoft-universal-printer-driver" data-raw-source="[Microsoft Universal Printer Driver](../print/microsoft-universal-printer-driver.md)">Microsoft 通用打印机驱动程序</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>打印：Microsoft 第 4 版打印机驱动程序</p></td>
<td align="left"></td>
<td align="left"><p>Windows 8 及更高版本</p></td>
<td align="left"><p>从 Windows 8 开始，Microsoft 提供了支持 PostScript 和非 PostScript 打印机以及绘图仪的单个内置类驱动程序。 该驱动程序可取代 Microsoft 绘图仪驱动程序、Microsoft 通用打印机驱动程序和 Microsoft PostScript 打印机驱动程序。 该打印机驱动程序可通过自身提供基本的打印支持，无需任何修改。 有关更多信息，请参阅 <a href="/windows-hardware/drivers/print/v4-printer-driver" data-raw-source="[V4 Printer Driver](../print/v4-printer-driver.md)">V4 打印机驱动程序</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>打印：Microsoft XPS 打印机驱动程序</p></td>
<td align="left"><p>XPSDrv</p></td>
<td align="left"><p>Windows Vista 及更高版本</p></td>
<td align="left"><p>Microsoft 通过 XPS 打印机驱动程序 (XPSDrv) 为打印 XPS 文档格式提供支持。 该驱动程序扩展了 Microsoft 基于 GDI 的第 3 版打印机驱动程序体系结构，支持使用 XML 纸张规范 (XPS) 文档。 通过 XPSDrv 打印机驱动程序，XPS 文档格式可用作后台打印文件格式和文档文件格式。 该 XPSDrv 打印机驱动程序可通过自身提供基本的 XPS 打印支持，无需任何修改。 有关详细信息，请参阅 <a href="/windows-hardware/drivers/print/xpsdrv-printer-drivers" data-raw-source="[XPSDrv Printer Drivers](../print/xpsdrv-printer-drivers.md)">XPSDrv 打印机驱动程序</a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>传感器：传感器 HID 类驱动程序</p></td>
<td align="left"><p>SensorsHIDClassDriver.dll</p></td>
<td align="left"><p>Windows 8 及更高版本</p></td>
<td align="left"><p>Microsoft 通过 HID 类驱动程序为运动、活动以及其他类型的传感器提供支持。 由于 Windows 8 包括此 HID 类驱动程序和相应的 HID I2C 及 HID USB 微型端口驱动程序，因此你不需要实现自己的驱动程序。 你只需在传感器的固件中，报告此白皮书中所描述的使用方法。 Windows 将使用你的固件及其 HID 驱动程序启用和初始化你的传感器，然后为相关 Windows API 提供访问该传感器的权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p>触摸：Windows 指针设备驱动程序</p></td>
<td align="left"></td>
<td align="left"><p>Windows 8 及更高版本</p></td>
<td align="left"><p>Microsoft 通过 HID 类驱动程序为笔和触摸设备提供支持。 由于 Windows 8 包括此 HID 类驱动程序和相应的 HID I2C 及 HID USB 微型端口驱动程序，因此你不需要实现自己的驱动程序。 你只需在指针设备的固件中报告此白皮书中描述的使用方法。 Windows 将使用你的固件及其 HID 驱动程序启用设备的触摸和指针功能，并为 Windows 触摸和指针 API 提供访问该设备的权限。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WPD：媒体传输协议类驱动程序</p></td>
<td align="left"><p>WpdMtpDr.dll、WpdMtp.dll、WpdMtpUs.dll、WpdConns.dll 和 WpdUsb.sys</p></td>
<td align="left"><p>Windows Vista 及更高版本</p></td>
<td align="left"><p>Microsoft 通过媒体传输协议类驱动程序为需要连接 Windows 的便携设备（例如，音乐播放器、数字相机、手机和健康监控设备）提供支持。 使用该类驱动程序的供应商必须在设备上实现 MTP 类协议。 （对于数码相机，MTP 实现应当向后兼容 PTP。）有关详细信息，请参阅<a href="/previous-versions/ff597573(v=vs.85)" data-raw-source="[Guidance for the Hardware Vendor](/previous-versions/ff597573(v=vs.85))">硬件供应商指南</a>。</p></td>
</tr>
</tbody>
</table>

 

