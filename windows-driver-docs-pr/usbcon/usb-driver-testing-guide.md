---
Description: 本部分介绍可用于测试您的 USB 硬件或软件、 捕获跟踪的操作和其他系统事件，并观察 USB 驱动程序堆栈由客户端驱动程序或应用程序发送的请求的响应方式的工具。
title: 在 Windows 中测试 USB 硬件、驱动程序和应用程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddb54a520aed50db51b5c7dc72ba51e5f0d2f641
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325737"
---
# <a name="testing-usb-hardware-drivers-and-apps-in-windows"></a>在 Windows 中测试 USB 硬件、驱动程序和应用程序


本部分介绍可用于测试您的 USB 硬件或软件、 捕获跟踪的操作和其他系统事件，并观察 USB 驱动程序堆栈由客户端驱动程序或应用程序发送的请求的响应方式的工具。

## <a name="in-this-section"></a>本节内容


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
<td><p><a href="microsoft-usb-test-tool--mutt--devices.md" data-raw-source="[Microsoft USB Test Tool (MUTT) devices](microsoft-usb-test-tool--mutt--devices.md)">Microsoft USB 测试工具 (MUTT) 设备</a></p></td>
<td><p>Microsoft USB 测试工具 (MUTT) 是用于测试您的 USB 硬件与 Microsoft USB 驱动程序堆栈的互操作性的设备的集合。 本部分提供了不同类型的 MUTT 设备、 测试可以运行使用该设备，并建议的控制器、 中心、 设备、 拓扑和 BIOS/UEFI 测试的简要概述。</p>
<p>若要与 MUTT 设备进行通信，需要 MUTT 软件包。 此包包含多个测试工具和让测试工程师测试互操作性 USB 控制器或与 Microsoft USB 驱动程序堆栈的中心的硬件的驱动程序。 测试工具验证 USB 主机控制器软件、 硬件 （包括固件） 和任何已安装主控制器和设备之间的 USB 集线器。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-test-tools.md" data-raw-source="[USB test tools](usb-test-tools.md)">USB 测试工具</a></p></td>
<td><p>介绍可用于测试 USB 设备和驱动程序的各种工具。</p></td>
</tr>
<tr class="odd">
<td><p><a href="test-usb-type-c-systems-with-mutt-connex-c.md" data-raw-source="[Test USB Type-C systems with USB Type-C ConnEx](test-usb-type-c-systems-with-mutt-connex-c.md)">测试与 USB 类型 C ConnEx USB C 类型系统</a></p></td>
<td><p>USB 类型 C 连接试验程序 (USB 类型 C ConnEx) 硬件转插板是 arduino 开发板的自定义防护罩。 防护罩提供四个开关来自动执行 USB 类型 C 方案的互操作性测试。</p></td>
</tr>
<tr class="even">
<td><p><a href="type.md" data-raw-source="[USB Type-C manual interoperability test procedures](type.md)">USB 类型 C 手动互操作性测试过程</a></p></td>
<td><p>本主题说明如何测试 USB 类型-C 启用系统和 Windows 的互操作性。 它用于执行各种功能的设备和系统制造商和压力测试系统和设备公开 USB 类型 C 连接器上提供指南。 本文假定读者熟悉的官方 USB 规范和 xHCI 互操作性测试过程，可以从 USB.ORG 下载。</p></td>
</tr>
<tr class="odd">
<td><p><a href="mutt-testing-options.md" data-raw-source="[How to prepare the test system to run MUTT test tools](mutt-testing-options.md)">如何进行准备，测试系统运行 MUTT 测试工具</a></p></td>
<td><p>在使用之前 MUTT 设备，必须准备的测试系统。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-run-stress-and-transfer-and-super-mutt-performance-tests-for-mutt-devices.md" data-raw-source="[How to run stress and transfer performance tests for MUTT devices](how-to-run-stress-and-transfer-and-super-mutt-performance-tests-for-mutt-devices.md)">如何运行压力和传输性能测试的 MUTT 设备</a></p></td>
<td><p>了解如何运行压力和传输和 SuperMUTT 性能测试。</p>
<p>压力和传输测试面向饱和总线协议和主机控制器软件。 这些测试执行多个同时进行的 I/O 传输和取消到 MUTT 设备。 MUTT 固件进行编程，这些测试中失败传输。 这些故障模拟错误条件的控制器或 USB 驱动程序堆栈紧张 USB 条件下，会面临。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-run-device-fundamental-tests-in-visual-studio-for-connected-mutt-devices.md" data-raw-source="[How to run system power devfund tests in Visual Studio for MUTT devices](how-to-run-device-fundamental-tests-in-visual-studio-for-connected-mutt-devices.md)">如何在 Visual Studio 中运行系统电源说明测试 MUTT 设备</a></p></td>
<td><p>介绍适用于连接到可用端口，MUTT 设备必须运行设备基础测试来执行压力和传输的测试和系统电源测试。</p>
<p>这些测试它们执行系统电源事件的同时执行简单的设备传输。 请注意，说明测试只能在 Windows 8 上运行。 您不能<a href="how-to-run-stress-and-transfer-and-super-mutt-performance-tests-for-mutt-devices.md" data-raw-source="[run stress and transfer tests](how-to-run-stress-and-transfer-and-super-mutt-performance-tests-for-mutt-devices.md)">运行压力和传输测试</a>并同时测试系统电源。 在单独的系统上执行这些测试。 但是，压力传输与系统之间切换电源测试。 为此，请完成第一组测试，重新启动计算机，然后按照下一个测试的说明进行操作。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-run-bios-uefi-testing-with-the-mutt-device.md" data-raw-source="[BIOS/UEFI testing with the MUTT devices](how-to-run-bios-uefi-testing-with-the-mutt-device.md)">BIOS/UEFI 使用 MUTT 设备进行测试</a></p></td>
<td><p>BIOS/UEFI 测试验证 USB 启动，并且切换到操作系统的控制器。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-run-hub-testing-with-the-mutt-device.md" data-raw-source="[Test USB hubs with MUTT devices](how-to-run-hub-testing-with-the-mutt-device.md)">使用 MUTT 设备测试 USB 集线器</a></p></td>
<td><p>中心测试的目标是从设备中生成一组完整的可能的通信模式。 你可以测试通过添加上游的 SuperMUTT 包来断开连接的方案。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-run-controller-and-device-testing-with-the-mutt-device.md" data-raw-source="[Test USB host controllers with MUTT devices](how-to-run-controller-and-device-testing-with-the-mutt-device.md)">使用 MUTT 设备测试 USB 主控制器</a></p></td>
<td><p>测试控制器的目标是从中心和设备生成一组完整的可能的通信模式。 这样，控制器和其固件要完全测试的内部状态。 MUTT 设备提供自动的方法，以生成各种可能的协议方案，可帮助测试。</p></td>
</tr>
<tr class="odd">
<td><p><a href="tools-in-the-package.md" data-raw-source="[Test USB devices with MUTT devices](tools-in-the-package.md)">测试与 MUTT 设备的 USB 设备</a></p></td>
<td><p>设备测试的目标是要测试针对各种中心方案的设备使用情况和系统电源状态。 MUTT 包和 SuperMUTT 包设备可以提供一种方法来公开设备以连接/断开跨不同中心的方案，以及系统电源状态方案。 当分别附加到 USB 2.0 和 3.0 版集线器中 MUTT 包和 SuperMUTT 包的设备，则测试设备。</p></td>
</tr>
<tr class="even">
<td><p><a href="windows-hardware-certification-kit-tests-for-usb.md" data-raw-source="[Windows Hardware Lab Kit Tests for USB](windows-hardware-certification-kit-tests-for-usb.md)">有关 USB 的 Windows 硬件实验室工具包测试</a></p></td>
<td><p>Windows 硬件 Lab Kit (HLK) 测试可以用于其他测试系统、 USB 主控制器、 中心和设备。 这些测试涵盖基本的设备功能、 可靠性和与 Windows 兼容性。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB)](https://msdn.microsoft.com/library/windows/hardware/ff538930)  



