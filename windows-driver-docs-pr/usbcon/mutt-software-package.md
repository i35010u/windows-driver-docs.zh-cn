---
description: MUTT 软件包包含多个工具，可用于 MUTT 设备。 工具套件包括固件升级应用程序、驱动程序安装包和向设备发送传输的应用程序。
title: MUTT 软件包中的工具
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7c495ce84967caac0278a124c3de939c9e38a18
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969322"
---
# <a name="tools-in-the-mutt-software-package"></a>MUTT 软件包中的工具


**上次更新时间：**

-   2019年2月

**适用于：**

-   Windows 10
-   Windows 8.1
-   Windows 8

MUTT 软件包包含多个工具，可用于 [MUTT 设备](microsoft-usb-test-tool--mutt--devices.md)。 工具套件包括固件升级应用程序、驱动程序安装包和向设备发送传输的应用程序。

## <a name="download-mutt-software-package"></a>下载 MUTT 软件包


Microsoft USB 测试工具 (MUTT) 软件包包含用于硬件测试工程师的测试工具，用于通过 Microsoft USB 驱动程序堆栈测试其 USB 控制器或集线器的互操作性。 随附的文档简要概述了不同类型的 MUTT 硬件，并为控制器、集线器、设备和 BIOS/UEFI 测试建议了拓扑。 该文档还包含有关如何运行测试、跟踪 USB 驱动程序堆栈中的事件以及在内核调试器中捕获信息的过程信息。

文件名： mutt2_94.msi

9.3 MB

[![下载 mutt 软件包](images/download.png)](https://go.microsoft.com/fwlink/p/?LinkId=786621)

## <a name="version-updates"></a>版本更新

版本2.9.4 的更改

- 更新 USB 类型-C SuperMUTT 固件 (v54) 
- 更新 USB 连接试验软件以使用 USB4 开关

版本2.9.3 的更改

- 修复驱动程序签名问题
- 包含 ARM64 测试工具

版本2.9 的更改

- 更新了 USB 类型-C SuperMUTT 固件 (v53) 

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

-   在版本1.9 及更早版本中，在某些系统上，SuperMutt 设备在连接到 xHCI 控制器时 (高速枚举，) 系统从 S4 恢复。 版本1.9.1 纠正了该问题。

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
<th>说明</th>
<th>文件名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="usbtcd.md" data-raw-source="[USBTCD](usbtcd.md)">USBTCD</a></td>
<td><ul>
<li>USBTCD 是一个应用程序 ( # A0) ，与内核模式驱动程序 ( # A1) 进行通信，并执行具有各种长度传输大小的常见 USB 数据传输方案。</li>
<li>驱动程序安装文件为 USBTCD 和 USBTCD。</li>
<li>FX3Perf.bat 度量 SuperMUTT 设备连接到的 USB 控制器的读取性能。</li>
</ul></td>
<td><p>USBTCD.exe</p>
<p>USBTCD.sys</p>
<p>USBTCD .inf</p>
<p>FX3Perf.bat</p>
<p>UsbTCDTransferTest.bat</p></td>
</tr>
<tr class="even">
<td></td>
<td><ul>
<li>收集有关系统上的 USB 3.0 主机控制器和 USB 3.0 集线器的信息，以确定有问题的固件修订和建议更新。</li>
<li>建议在进行任何其他测试之前运行此测试，以筛选已知问题。 仅在 Windows 8 上运行。</li>
</ul></td>
<td>xhciwmi.exe</td>
</tr>
<tr class="odd">
<td><a href="usb-xhciwmi.md" data-raw-source="[XHCIWMI](usb-xhciwmi.md)">XHCIWMI</a><a href="usblpm-tool.md" data-raw-source="[USBLPM](usblpm-tool.md)">USBLPM</a></td>
<td><ul>
<li>监视 USB 3.0 端口的 U0/U1/U2/U3 电源状态。</li>
<li>它验证 U0/U1/U2 之间的转换是否正常进行。</li>
</ul></td>
<td>UsbLPM.exe</td>
</tr>
<tr class="even">
<td><a href="usbstress.md" data-raw-source="[USBStress](usbstress.md)">USBStress</a></td>
<td><ul>
<li>USBStress 应用程序与内核模式驱动程序通信 ( # A0) 并执行常见的 USB 数据传输方案。</li>
<li>驱动程序安装文件为 usbstress.sys 和 usbstress。</li>
<li>安装驱动程序后，UsbStressTest 文件将运行所有数据传输测试。</li>
</ul></td>
<td><p>usbstress.exe</p>
<p>usbstress .inf</p>
<p>usbstress.sys</p>
<p>UsbStressTest.bat</p></td>
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
<td><p>MuttUtil.exe</p></td>
</tr>
<tr class="even">
<td><a href="how-to-retrieve-information-about-a-usb-device.md" data-raw-source="[USB hardware verifier](how-to-retrieve-information-about-a-usb-device.md)">USB 硬件验证程序</a></td>
<td>显示控制台上的所有硬件事件。</td>
<td>USB3HWVerifierAnalyzer.exe</td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[USB](https://docs.microsoft.com/windows-hardware/drivers/)  
[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)  



