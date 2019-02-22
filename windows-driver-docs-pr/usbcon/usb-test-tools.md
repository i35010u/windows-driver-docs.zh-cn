---
Description: Describes various tools you can use to test USB devices and drivers.
title: USB 测试工具
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17b3155c1af400918332470821c43df3d9b82358
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555296"
---
# <a name="usb-test-tools"></a>USB 测试工具


介绍可用于测试 USB 设备和驱动程序的各种工具。

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
<td><p><a href="muttutil.md" data-raw-source="[MuttUtil](muttutil.md)">MuttUtil</a></p></td>
<td><p>MuttUtil 上执行各种任务<a href="microsoft-usb-test-tool--mutt--devices.md" data-raw-source="[MUTT devices](microsoft-usb-test-tool--mutt--devices.md)">MUTT 设备</a>。</p>
<ul>
<li>更新测试设备的固件。</li>
<li>安装 MUTT 设备的驱动程序。</li>
<li>验证设备安装未出现错误。</li>
<li>更改设备的运行总线速度。</li>
<li>将设备配置为在指定的时间段后发送恢复唤醒信号。</li>
<li>对于 MUTT 包，它用于设置要以完整或高的速度; 运行的中心为单 TT 或多 TT 中心。</li>
</ul>
<p>MuttUtil 嵌入中包括的测试脚本，以确保测试设备正确升级到最新的固件的安装部分。 该工具包含在<a href="https://go.microsoft.com/fwlink/p/?linkid=617710" data-raw-source="[MUTT Software Package](https://go.microsoft.com/fwlink/p/?linkid=617710)">MUTT 软件包</a>。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-send-a-usb-device-to-select-suspend.md" data-raw-source="[USB client driver verifier](how-to-send-a-usb-device-to-select-suspend.md)">USB 客户端驱动程序验证工具</a></p></td>
<td><p>本主题介绍 USB 客户端驱动程序验证工具功能，客户端驱动程序来测试某些失败的情况下的 USB 3.0 驱动程序堆栈。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-retrieve-information-about-a-usb-device.md" data-raw-source="[USB hardware verifier (USB3HWVerifierAnalyzer.exe)](how-to-retrieve-information-about-a-usb-device.md)">USB 硬件验证工具 (USB3HWVerifierAnalyzer.exe)</a></p></td>
<td><p>本主题介绍用于测试和调试特定硬件事件的 USB 硬件验证程序工具 (USB3HWVerifierAnalyzer.exe)。</p></td>
</tr>
<tr class="even">
<td><p><a href="usblpm-tool.md" data-raw-source="[USBLPM](usblpm-tool.md)">USBLPM</a></p></td>
<td><p>USBLPM 工具监视 USB 3.0 端口 U0/U1/U2/U3 电源的状态。 此外可以用于验证正确发生 U0/U1/U2 之间的转换。 此外，该工具可以启用或禁用系统中的所有设备上的 U1 和/或 U2 状态。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usbstress.md" data-raw-source="[USBStress](usbstress.md)">USBStress</a></p></td>
<td><p>USBStress 是用户模式应用程序 (usbstress.exe) 和内核模式驱动程序的驱动程序安装包的组合 usbstress.sys。</p></td>
</tr>
<tr class="even">
<td><p><a href="usbtcd.md" data-raw-source="[USBTCD](usbtcd.md)">USBTCD</a></p></td>
<td><p>USBTCD 是用户模式应用程序和内核模式驱动程序的组合。 此工具将执行读取和写入操作。 初始化控件，大容量、 等时，数据传输的各种传输长度与测试设备。 对于 SuperMUTT 设备，USBTCD 将数据传输到流支持的大容量终结点。 它还可以作为链接 MDLs 发送的传输缓冲区。 在这种情况下，您可以传输缓冲区中指定的段数。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-xhciwmi.md" data-raw-source="[USB XHCIWMI](usb-xhciwmi.md)">USB XHCIWMI</a></p></td>
<td><p>XHCIWMI 是一个工具用于诊断目的。 此工具仅在 Windows 8 上运行并收集信息时与设备附加到 xHCI 端口和 Windows 加载 Microsoft USB 3.0 驱动程序堆栈。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[USB 诊断和测试指南](usb-driver-testing-guide.md)  



