---
Description: MUTT 软件包包含多个工具，可用于 MUTT 设备。 工具套件包括固件升级应用程序、驱动程序安装包和向设备发送传输的应用程序。
title: MUTT 软件包中的工具
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb006513d071d7f7ca8a5cb8919df593ed9e0b76
ms.sourcegitcommit: b7ba0d42117f30125ae2dcd4dcb16dd988a18ff3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2019
ms.locfileid: "72303925"
---
# <a name="tools-in-the-mutt-software-package"></a>MUTT 软件包中的工具


**上次更新时间：**

-   2019年2月

**适用对象：**

-   Windows 10
-   Windows 8.1
-   Windows 8

MUTT 软件包包含多个工具，可用于[MUTT 设备](microsoft-usb-test-tool--mutt--devices.md)。 工具套件包括固件升级应用程序、驱动程序安装包和向设备发送传输的应用程序。

## <a name="download-mutt-software-package"></a>下载 MUTT 软件包


Microsoft USB 测试工具（MUTT）软件包包含测试工具，可供硬件测试工程师通过 Microsoft USB 驱动程序堆栈测试其 USB 控制器或集线器的互操作性。 随附的文档简要概述了不同类型的 MUTT 硬件，并为控制器、集线器、设备和 BIOS/UEFI 测试建议了拓扑。 该文档还包含有关如何运行测试、跟踪 USB 驱动程序堆栈中的事件以及在内核调试器中捕获信息的过程信息。

文件名： mutt2_94 .msi

9.3 MB

[![下载 mutt 软件包](images/download.png)](https://go.microsoft.com/fwlink/p/?LinkId=786621)

## <a name="version-updates"></a>版本更新

版本2.9.4 的更改

- 更新 USB 类型-C SuperMUTT 固件（v54）
- 更新 USB 连接试验软件以使用 USB4 开关

版本2.9.3 的更改

- 修复驱动程序签名问题
- 包含 ARM64 测试工具

版本2.9 的更改

- 已更新的 USB 类型-C SuperMUTT 固件（v53）

版本2.8 的更改

- 更新了 USB 类型 C SuperMUTT 固件，以改善与 HLK UCSI 测试的兼容性。

版本2.7 的更改

- 更新了 USB 类型-C SuperMUTT 固件、工具和文档。 与 HLK UCSI 测试兼容。

版本2.4 的更改

-   包括 USB 类型 C SuperMUTT 固件、工具和文档的初始放置。

版本2.2 的更改

-   包含 USB 连接试验工具

版本2.0 的更改

-   已将 SuperMUTT 固件更新到版本45。
-   已更新 WinUSB 传输测试。

版本1.9.1 的更改

-   在版本1.9 及更早版本中，在某些系统上，SuperMutt 设备在系统从 S4 恢复之后会高速（连接到 xHCI 控制器时）进行枚举。 版本1.9.1 纠正了该问题。

版本1.9 的更改

-   默认情况下，SuperMUTT 通过读取设备的 MS OS 描述符加载 WinUSB 驱动程序。
-   默认情况下，使用 WinUSB 的 SuperMUTT 支持选择性挂起。

## <a name="tools-in-the-package"></a>包中的工具


<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>测试工具</th>
<th>描述</th>
<th>Filename</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="usbtcd.md" data-raw-source="[USBTCD](usbtcd.md)">USBTCD</a></td>
<td><ul>
<li>USBTCD 是一个应用程序（USBTCD），该应用程序与内核模式驱动程序（USBTCD）进行通信，并执行各种长度的传输大小的常用 USB 数据传输方案。</li>
<li>驱动程序安装文件为 USBTCD 和 USBTCD。</li>
<li>FX3Perf 测量 SuperMUTT 设备连接到的 USB 控制器的读取性能。</li>
</ul></td>
<td><p>USBTCD</p>
<p>USBTCD</p>
<p>USBTCD .inf</p>
<p>FX3Perf</p>
<p>UsbTCDTransferTest</p></td>
</tr>
<tr class="even">
<td></td>
<td><ul>
<li>收集有关系统上的 USB 3.0 主机控制器和 USB 3.0 集线器的信息，以确定有问题的固件修订和建议更新。</li>
<li>建议在进行任何其他测试之前运行此测试，以筛选已知问题。 仅在 Windows 8 上运行。</li>
</ul></td>
<td>xhciwmi</td>
</tr>
<tr class="odd">
<td><a href="usb-xhciwmi.md" data-raw-source="[XHCIWMI](usb-xhciwmi.md)">XHCIWMI</a><a href="usblpm-tool.md" data-raw-source="[USBLPM](usblpm-tool.md)">USBLPM</a></td>
<td><ul>
<li>监视 USB 3.0 端口的 U0/U1/U2/U3 电源状态。</li>
<li>它验证 U0/U1/U2 之间的转换是否正常进行。</li>
</ul></td>
<td>UsbLPM</td>
</tr>
<tr class="even">
<td><a href="usbstress.md" data-raw-source="[USBStress](usbstress.md)">USBStress</a></td>
<td><ul>
<li>USBStress 应用程序与内核模式驱动程序（USBStress）进行通信，并执行常见的 USB 数据传输方案。</li>
<li>驱动程序安装文件为 usbstress 和 usbstress。</li>
<li>安装驱动程序后，UsbStressTest 文件将运行所有数据传输测试。</li>
</ul></td>
<td><p>usbstress</p>
<p>usbstress .inf</p>
<p>usbstress</p>
<p>UsbStressTest</p></td>
</tr>
<tr class="odd">
<td><a href="muttutil.md" data-raw-source="[MuttUtil](muttutil.md)">MuttUtil</a></td>
<td><ul>
<li>更新测试设备的固件。</li>
<li>安装适用于 MUTT 设备的驱动程序。</li>
<li>验证是否安装了设备且没有错误。</li>
<li>更改设备的操作总线速度。</li>
<li>将设备配置为在指定的时间段后发送恢复唤醒信号。</li>
<li>对于 MUTT Pack，它会将集线器设置为全速或高速操作;作为单 TT 或多 TT 中心。</li>
</ul></td>
<td><p>MuttUtil</p></td>
</tr>
<tr class="even">
<td><a href="how-to-retrieve-information-about-a-usb-device.md" data-raw-source="[USB hardware verifier](how-to-retrieve-information-about-a-usb-device.md)">USB 硬件验证程序</a></td>
<td>显示控制台上的所有硬件事件。</td>
<td>USB3HWVerifierAnalyzer</td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[USB](https://docs.microsoft.com/windows-hardware/drivers/)  
[Microsoft USB 测试工具（MUTT）设备](microsoft-usb-test-tool--mutt--devices.md)  



