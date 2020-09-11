---
description: 用途：本部分介绍 Windows 操作系统中的通用串行总线 (USB) 支持，以便你开发可与 Windows 互操作的 USB 设备驱动程序。
title: 为 USB 设备开发 Windows 客户端驱动程序的概述
ms.date: 01/07/2019
ms.localizationpriority: High
ms.openlocfilehash: 6023d0202702d71dfe3a97c30f8dc3e5a88909f3
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010067"
---
# <a name="overview-of-developing-windows-client-drivers-for-usb-devices"></a>为 USB 设备开发 Windows 客户端驱动程序的概述


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>用途</strong></p>
<p>本部分介绍 Windows 操作系统中的通用串行总线 (USB) 支持，以便你开发可与 Windows 互操作的 USB 设备驱动程序。</p>
<p><strong>如果适用</strong></p>
<p>USB 设备是通过单个端口连接到计算机的外设，例如鼠标设备和键盘。 USB 客户端驱动程序是计算机上安装的软件，该软件与硬件通信以使设备正常运行。 如果设备属于 Microsoft 支持的设备类，Windows 会为该设备加载 <a href="system-supplied-usb-drivers.md" data-raw-source="[Microsoft-provided USB drivers](system-supplied-usb-drivers.md)">Microsoft 提供的 USB 驱动程序</a>（随机类驱动程序）之一。 否则，自定义客户端驱动程序必须由硬件制造商或第三方供应商提供。 当 Windows 第一次检测到该设备时，用户会为该设备安装客户端驱动程序。 成功安装后，Windows 将在每次连接该设备时加载此客户端驱动程序，并在该设备与主计算机断开连接时卸载此驱动程序。</p>
<p>可以通过使用 <a href="/windows-hardware/drivers/wdf/" data-raw-source="[Windows Driver Frameworks](/windows-hardware/drivers/wdf/)">Windows 驱动程序框架</a> (WDF) 或 <a href="/windows-hardware/drivers/kernel/windows-driver-model" data-raw-source="[Windows Driver Model](/windows-hardware/drivers/kernel/windows-driver-model)">Windows 驱动程序模型</a> (WDM) 来开发 USB 设备的自定义客户端驱动程序。 大多数客户端驱动程序将其请求发送到 Microsoft 提供的 USB 驱动程序堆栈（该堆栈进行硬件抽象层 (HAL) 函数调用，以便将客户端驱动程序的请求发送到硬件），而不是直接与硬件通信。 本部分中的主题介绍客户端驱动程序可以发送的典型请求，以及客户端驱动程序为创建这些请求而必须调用的设备驱动程序接口 (DDI)。</p>
<p><strong>开发人员受众</strong></p>
<p>USB 设备的客户端驱动程序是一个 WDF 或 WDM 驱动程序，它通过由 USB 驱动程序堆栈公开的 DDI 与设备进行通信。 本部分供已熟悉 WDM 的 C/C++ 程序员使用。 使用此部分之前，应了解基本的驱动程序开发。 有关详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/index" data-raw-source="[Getting Started with Windows Drivers](../gettingstarted/index.md)">Windows 驱动程序入门</a>。 对于 WDF 驱动程序，客户端驱动程序可以使用专门用于处理 USB 目标的<a href="/windows-hardware/drivers/debugger/kernel-mode-driver-framework-debugging" data-raw-source="[Kernel-Mode Driver Framework](/windows-hardware/drivers/debugger/kernel-mode-driver-framework-debugging)">内核模式驱动程序框架</a> (KMDF) 或<a href="/windows-hardware/drivers/wdf/" data-raw-source="[User-Mode Driver Framework](/windows-hardware/drivers/wdf/)">用户模式驱动程序框架</a> (UMDF) 接口。 有关 USB 特定接口的详细信息，请参阅 <a href="/windows-hardware/drivers/ddi/wdfusb/" data-raw-source="[WDF USB Reference](/windows-hardware/drivers/ddi/wdfusb/)">WDF USB 参考</a>和 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/" data-raw-source="[UMDF USB I/O Target Interfaces](/windows-hardware/drivers/ddi/wudfddi/)">UMDF USB I/O 目标接口</a>。</p>
<p><strong>开发工具</strong></p>
<p>Windows 驱动程序工具包 (WDK) 包含开发驱动程序所需的资源，如头文件、库、工具和示例。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=617155" data-raw-source="[Download kits and tools for Windows](https://go.microsoft.com/fwlink/p/?linkid=617155)">下载适用于 Windows 的工具包和工具</a></p>
<p><strong>USB 编程参考</strong></p>
<p>提供 USB 客户端驱动程序所使用的 I/O 请求、支持例程、结构和接口的规范。 这些例程和相关的数据结构在 WDK 头文件中定义。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#common-usb-client-driver-reference" data-raw-source="[Universal Serial Bus (USB) programming reference](/windows-hardware/drivers/ddi/_usbref/#common-usb-client-driver-reference)">通用串行总线 (USB) 编程参考</a>。</p>
<p><strong>USB 驱动程序示例</strong></p>
<p>使用这些示例可开始着手 USB 客户端驱动程序编程。</p>
<ul>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=617157" data-raw-source="[Usbsamp Generic USB Driver]( https://go.microsoft.com/fwlink/p/?linkid=617157)">Usbsamp 通用 USB 驱动程序</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=617158" data-raw-source="[Sample KMDF Function Driver for OSR USB-FX2](https://go.microsoft.com/fwlink/p/?linkid=617158)">OSR USB-FX2 的示例 KMDF 函数驱动程序</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?LinkId=618002" data-raw-source="[Sample UMDF Function Driver for OSR USB-FX2](https://go.microsoft.com/fwlink/p/?LinkId=618002)">OSR USB-FX2 的示例 UMDF 函数驱动程序</a></li>
</ul>
<p><strong>相关标准与规范</strong></p>
<p>可以从<a href="https://go.microsoft.com/fwlink/p/?linkid=224892" data-raw-source="[Universal Serial Bus Documents]( https://go.microsoft.com/fwlink/p/?linkid=224892)">通用串行总线文档</a>网站下载官方 USB 规范。 此网站包含“通用串行总线修订版 3.0 规范”和“通用串行总线修订版 2.0 规范”的链接。</p></td>
<td><p><strong>文档部分</strong></p>
<p><a href="getting-started-with-usb-client-driver-development.md" data-raw-source="[Getting started with USB client driver development](getting-started-with-usb-client-driver-development.md)">USB 客户端驱动程序开发入门</a></p>
USB 驱动程序开发简介。 介绍在为设备提供 USB 驱动程序时如何选择最适合的模型。
使用 Microsoft Visual Studio 随附的 USB 模板编写、生成并安装你的第一个主干用户模式和内核模式 USB 驱动程序。
<p><a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers in Windows](usb-3-0-driver-stack-architecture.md)">Windows 中的 USB 主机端驱动程序</a></p>
提供 USB 驱动程序堆栈体系结构的概述。
<p><a href="communicating-with-a-usb-device.md" data-raw-source="[About USB Block Requests (URBs)](communicating-with-a-usb-device.md)">关于 USB 块请求 (URB)</a></p>
了解客户端驱动程序如何构建称为 USB 请求块 (URB) 的可变长度数据结构，以便将请求提交到 USB 驱动程序堆栈。
<p><a href="usb-descriptors.md" data-raw-source="[USB descriptors](usb-descriptors.md)">USB 描述符</a></p>
了解客户端驱动程序如何构建称为 USB 请求块 (URB) 的可变长度数据结构，以便将请求提交到 USB 驱动程序堆栈。
<p><a href="configuring-usb-devices.md" data-raw-source="[Selecting a USB configuration in USB drivers](configuring-usb-devices.md)">选择 USB 驱动程序中的 USB 配置</a></p>
设备配置指的是客户端驱动程序执行的任务，用于选择 USB 配置和每个接口中的备用接口。 该部分显示了选择 USB 配置所需的方法调用。
<p><a href="usb-device-i-o.md" data-raw-source="[Sending USB data transfers in USB client drivers](usb-device-i-o.md)">在 USB 客户端驱动程序中发送 USB 数据传输</a></p>
介绍 USB 管道、I/O 请求的 URB，以及客户端驱动程序如何使用设备驱动程序接口 (DDI) 将数据传入和传出 USB 设备。
<p><a href="usb-power-management.md" data-raw-source="[Implementing power management in USB client drivers](usb-power-management.md)">在 USB 客户端驱动程序中实施电源管理</a></p>
使用符合通用串行总线 (USB) 规范的 USB 设备的电源管理功能，这是一组丰富且复杂的电源管理功能。</td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB)](../index.yml)