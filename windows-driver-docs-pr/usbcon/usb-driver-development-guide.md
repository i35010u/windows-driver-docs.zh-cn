---
Description: PurposeThis 部分介绍 Windows 操作系统中的通用串行总线 (USB) 支持，以便可以开发可与 Windows 互操作的 USB 设备驱动程序。
title: 为 USB 设备开发 Windows 客户端驱动程序
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: f5e1e0b0e3663bf166becbb658f636dacce4035e
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394135"
---
# <a name="developing-windows-client-drivers-for-usb-devices"></a>为 USB 设备开发 Windows 客户端驱动程序


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>用途</strong></p>
<p>本部分介绍 Windows 操作系统中的通用串行总线 (USB) 支持，以便可以开发可与 Windows 互操作的 USB 设备驱动程序。</p>
<p><strong>在适用的情况</strong></p>
<p>外围设备，如鼠标设备和键盘，连接到通过单个端口的计算机的 USB 设备。 USB 客户端驱动程序是与硬件即可使设备函数进行通信的计算机上安装的软件。 如果设备属于 Microsoft 支持的设备类，Windows 将加载之一<a href="system-supplied-usb-drivers.md" data-raw-source="[Microsoft-provided USB drivers](system-supplied-usb-drivers.md)">由 Microsoft 提供的 USB 驱动程序</a>（中的内置类驱动程序） 的设备。 否则为自定义客户端驱动程序必须由硬件制造商提供或第三方供应商。 当 Windows 首次检测到该设备时，用户安装设备的客户端驱动程序。 安装成功后，Windows 将加载客户端驱动程序每次设备附加和分离设备时从主计算机卸载该驱动程序。</p>
<p>可以通过使用开发 USB 设备的自定义客户端驱动程序<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/" data-raw-source="[Windows Driver Frameworks](https://docs.microsoft.com/windows-hardware/drivers/wdf/)">Windows 驱动程序框架</a>(WDF) 或<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model" data-raw-source="[Windows Driver Model](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)">Windows 驱动程序模型</a>(WDM)。 而不是直接与硬件通信，大多数客户端驱动程序将其请求发送到由 Microsoft 提供的 USB 驱动程序堆栈进行硬件抽象层 (HAL) 函数调用将客户端驱动程序的请求发送到的硬件。 在本部分中的主题介绍典型的客户端驱动程序可以发送的请求和客户端驱动程序必须调用来创建这些请求的设备驱动程序接口 (DDIs)。</p>
<p><strong>开发人员受众</strong></p>
<p>USB 设备的客户端驱动程序是与 DDIs 公开的 USB 驱动程序堆栈通过设备进行通信的 WDF 或 WDM 驱动程序。 本部分旨在通过 C 使用 /C++的编程人员熟悉 WDM。 使用本部分之前，应了解基本的驱动程序开发。 有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/index" data-raw-source="[Getting Started with Windows Drivers](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/index)">开始使用 Windows 驱动程序</a>。 有关 WDF 驱动程序，客户端驱动程序可以使用<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-debugging" data-raw-source="[Kernel-Mode Driver Framework](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-debugging)">内核模式驱动程序框架</a>(KMDF) 或<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/" data-raw-source="[User-Mode Driver Framework](https://docs.microsoft.com/windows-hardware/drivers/wdf/)">用户模式驱动程序框架</a>专门用于使用 USB 目标 (UMDF) 接口。 有关特定于 USB 的接口的详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/" data-raw-source="[WDF USB Reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/)">WDF USB 引用</a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/" data-raw-source="[UMDF USB I/O Target Interfaces](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/)">UMDF USB I/O 目标接口</a>。</p>
<p><strong>开发工具</strong></p>
<p>Windows Driver Kit (WDK) 包含所需的驱动程序开发，例如标头、 库、 工具和示例的资源。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=617155" data-raw-source="[Download kits and tools for Windows](https://go.microsoft.com/fwlink/p/?linkid=617155)">下载适用于 Windows 的工具包和工具</a></p>
<p><strong>USB 编程参考</strong></p>
<p>提供用于 I/O 请求、 支持例程、 结构和使用的 USB 客户端驱动程序接口规范。 WDK 标头中定义这些例程和相关的数据结构。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#common-usb-client-driver-reference" data-raw-source="[Universal Serial Bus (USB) programming reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#common-usb-client-driver-reference)">通用串行总线 (USB) 编程参考</a>。</p>
<p><strong>USB 驱动程序示例</strong></p>
<p>使用这些示例，若要开始使用 USB 客户端驱动程序编程。</p>
<ul>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=617157" data-raw-source="[Usbsamp Generic USB Driver]( https://go.microsoft.com/fwlink/p/?linkid=617157)">Usbsamp 泛型 USB 驱动程序</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=617158" data-raw-source="[Sample KMDF Function Driver for OSR USB-FX2](https://go.microsoft.com/fwlink/p/?linkid=617158)">OSR USB FX2 示例 KMDF 函数驱动程序</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?LinkId=618002" data-raw-source="[Sample UMDF Function Driver for OSR USB-FX2](https://go.microsoft.com/fwlink/p/?LinkId=618002)">OSR USB FX2 示例 UMDF 函数驱动程序</a></li>
</ul>
<p><strong>相关的标准和规范</strong></p>
<p>您可以下载从官方 USB 规范<a href="https://go.microsoft.com/fwlink/p/?linkid=224892" data-raw-source="[Universal Serial Bus Documents]( https://go.microsoft.com/fwlink/p/?linkid=224892)">通用串行总线文档</a>网站。 此网站包含通用串行总线修订版本 3.0 规范和通用串行总线修订版本 2.0 规范的链接。</p></td>
<td><p><strong>文档部分</strong></p>
<p><a href="getting-started-with-usb-client-driver-development.md" data-raw-source="[Getting started with USB client driver development](getting-started-with-usb-client-driver-development.md)">USB 客户端驱动程序开发入门</a></p>
USB 驱动程序开发简介。 介绍在为设备提供 USB 驱动程序时如何选择最适合的模型。
编写、 构建和使用 Microsoft Visual Studio 附带的 USB 模板安装第一个主干用户模式和内核模式 USB 驱动程序。
<p><a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers in Windows](usb-3-0-driver-stack-architecture.md)">在 Windows 中的 USB 宿主端驱动程序</a></p>
提供 USB 驱动程序堆栈体系结构的概述。
<p><a href="communicating-with-a-usb-device.md" data-raw-source="[About USB Block Requests (URBs)](communicating-with-a-usb-device.md)">有关 USB 块请求 (URBs)</a></p>
了解客户端驱动程序生成称为 USB 请求块 (URB) 以将请求提交到 USB 驱动程序堆栈的可变长度数据结构的方式。
<p><a href="usb-descriptors.md" data-raw-source="[USB descriptors](usb-descriptors.md)">USB 描述符</a></p>
了解客户端驱动程序生成称为 USB 请求块 (URB) 以将请求提交到 USB 驱动程序堆栈的可变长度数据结构的方式。
<p><a href="configuring-usb-devices.md" data-raw-source="[Selecting a USB configuration in USB drivers](configuring-usb-devices.md)">在 USB 驱动程序选择 USB 配置</a></p>
设备配置是指客户端驱动程序执行要选择的每个接口中的 USB 配置和备用接口的任务。 方法调用所需选择 USB 配置节所示。
<p><a href="usb-device-i-o.md" data-raw-source="[Sending USB data transfers in USB client drivers](usb-device-i-o.md)">USB 客户端驱动程序中的发送 USB 数据传输</a></p>
介绍 USB 管道、 URBs 的 I/O 请求和客户端驱动程序如何使用设备驱动程序接口 (DDIs) 将数据传入和传出的 USB 设备。
<p><a href="usb-power-management.md" data-raw-source="[Implementing power management in USB client drivers](usb-power-management.md)">在 USB 客户端驱动程序中实施电源管理</a></p>
使用符合通用串行总线 (USB) 规范的 USB 设备的电源管理功能已编写了一个丰富的和复杂的电源管理功能设置。</td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  



