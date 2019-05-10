---
Description: MUTT 软件包包含几个工具与 MUTT 设备一起使用。 工具套件包括固件升级应用程序、 驱动程序安装包和应用程序发送到设备的传输。
title: MUTT 软件包中的工具
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd9488de20bff07db101f10c8e443a35f349537f
ms.sourcegitcommit: 952c17357bd2dd91a4caad42313a063951317697
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65515037"
---
# <a name="tools-in-the-mutt-software-package"></a>MUTT 软件包中的工具


**上次更新时间：**

-   2019 年 2 月，

**适用于：**

-   Windows 10
-   Windows 8.1
-   Windows 8

MUTT 软件包包含几个工具可与[MUTT 设备](microsoft-usb-test-tool--mutt--devices.md)。 工具套件包括固件升级应用程序、 驱动程序安装包和应用程序发送到设备的传输。

## <a name="download-mutt-software-package"></a>下载 MUTT 软件包


Microsoft USB 测试工具 (MUTT) 软件程序包中包含硬件测试工程师，若要测试其 USB 控制器或中心与 Microsoft USB 驱动程序堆栈的互操作性测试的工具。 包含的文档提供了不同类型的 MUTT 硬件的简要概述，并建议的控制器、 中心、 设备和 BIOS/UEFI 测试拓扑。 文档还包含有关如何运行测试、 跟踪事件中 USB 驱动程序堆栈，并捕获内核调试程序中的信息的过程信息。

文件名： mutt2_93.msi

9.1 MB

[![下载 mutt 软件包](images/download.png)](https://go.microsoft.com/fwlink/p/?LinkId=786621)

## <a name="version-updates"></a>版本更新

更改版本 2.9.3

- 修复驱动程序签名问题
- 包括 ARM64 测试工具

更改用于版本 2.9

- 已更新的 USB 类型 C SuperMUTT 固件 (v53)

版本 2.8 的更改

- 已改进使用 HLK UCSI 测试的兼容性的 USB 类型 C SuperMUTT 固件更新。

更改版本 2.7

- 更新 USB 类型 C SuperMUTT 固件、 工具和文档。 与 HLK UCSI 测试兼容。

对于版本 2.4 的更改

-   包括 USB 类型 C SuperMUTT 固件、 工具和文档的初始下拉。

对于版本 2.2 的更改

-   包括 USB 连接试验程序工具

对于 2.0 版的更改

-   已更新到版本 45 SuperMUTT 固件。
-   已更新的 WinUSB 传输测试。

更改版本 1.9.1

-   在版本 1.9 及更早版本，在某些系统中后系统, 枚举 （当连接到 xHCI 控制器） 的高速 SuperMutt 设备从 S4 中恢复。 版本 1.9.1 更正该问题。

1.9 版的更改

-   SuperMUTT 读取设备的 MS OS 描述符，默认情况下加载 WinUSB 驱动程序。
-   默认情况下，与 WinUSB 支持选择性 superMUTT 挂起。

## <a name="tools-in-the-package"></a>在包中的工具


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
<li>USBTCD 是一个应用程序 (USBTCD.exe) 与内核模式驱动程序 (USBTCD.sys) 进行通信并执行常见 USB 数据传输的方案与不同长度的传输大小。</li>
<li>驱动程序安装文件是 USBTCD.sys 和 USBTCD.inf。</li>
<li>FX3Perf.bat 测量 SuperMUTT 设备附加到的 USB 控制器的读取的性能。</li>
</ul></td>
<td><p>USBTCD.exe</p>
<p>USBTCD.sys</p>
<p>USBTCD.inf</p>
<p>FX3Perf.bat</p>
<p>UsbTCDTransferTest.bat</p></td>
</tr>
<tr class="even">
<td></td>
<td><ul>
<li>为了确定有问题的固件版本并建议更新系统上收集有关 USB 3.0 主机控制器和 USB 3.0 集线器的信息。</li>
<li>我们建议运行此测试之前任何其他测试来筛选的已知的问题。 仅在 Windows 8 上运行。</li>
</ul></td>
<td>xhciwmi.exe</td>
</tr>
<tr class="odd">
<td><a href="usb-xhciwmi.md" data-raw-source="[XHCIWMI](usb-xhciwmi.md)">XHCIWMI</a><a href="usblpm-tool.md" data-raw-source="[USBLPM](usblpm-tool.md)">USBLPM</a></td>
<td><ul>
<li>监视 USB 3.0 端口 U0/U1/U2/U3 电源状态。</li>
<li>它验证 U0/U1/U2 之间的转换会正确进行。</li>
</ul></td>
<td>UsbLPM.exe</td>
</tr>
<tr class="even">
<td><a href="usbstress.md" data-raw-source="[USBStress](usbstress.md)">USBStress</a></td>
<td><ul>
<li>USBStress 应用程序与内核模式驱动程序 (usbstress.sys) 通信，并执行常见的 USB 数据传输方案。</li>
<li>驱动程序安装文件是 usbstress.sys 和 usbstress.inf。</li>
<li>安装该驱动程序后，UsbStressTest 文件将传输的所有数据都运行测试。</li>
</ul></td>
<td><p>usbstress.exe</p>
<p>usbstress.inf</p>
<p>usbstress.sys</p>
<p>UsbStressTest.bat</p></td>
</tr>
<tr class="odd">
<td><a href="muttutil.md" data-raw-source="[MuttUtil](muttutil.md)">MuttUtil</a></td>
<td><ul>
<li>更新测试设备的固件。</li>
<li>安装 MUTT 设备的驱动程序。</li>
<li>验证设备安装未出现错误。</li>
<li>更改设备的运行总线速度。</li>
<li>将设备配置为在指定的时间段后发送恢复唤醒信号。</li>
<li>对于 MUTT 包，它用于设置要以完整或高的速度; 运行的中心为单 TT 或多 TT 中心。</li>
</ul></td>
<td><p>MuttUtil.exe</p></td>
</tr>
<tr class="even">
<td><a href="how-to-retrieve-information-about-a-usb-device.md" data-raw-source="[USB hardware verifier](how-to-retrieve-information-about-a-usb-device.md)">USB 硬件验证工具</a></td>
<td>在控制台上显示所有硬件事件。</td>
<td>USB3HWVerifierAnalyzer.exe</td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[USB](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)  



