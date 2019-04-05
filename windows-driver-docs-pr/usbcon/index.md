---
Description: 通用串行总线 (USB) 提供了一个可扩展且可热插拔的即插即用串行接口，可确保为键盘、鼠标、游戏杆、打印机、扫描仪、存储设备、调制解调器和视频会议摄像机之类的外设提供标准的低成本连接。 对于所有使用旧端口（例如 PS/2 端口、串行端口和并行端口）的外围设备，建议迁移到 USB。 USB-IF 是一个特别兴趣组 (SIG)，负责维护官方 USB 规范、测试规范和工具。 Windows 操作系统为 USB 主控制器、集线器以及符合官方 USB 规范的设备和系统提供本机支持。 Windows 还提供编程接口，用于开发可与 USB 设备通信的设备驱动程序和应用程序。
title: 通用串行总线 (USB)
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 05c1d2431db9ecc94f0b7d59da601970deab542c
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349572"
---
# <a name="universal-serial-bus-usb"></a>通用串行总线 (USB)


通用串行总线 (USB) 提供了一个可扩展且可热插拔的即插即用串行接口，可确保为键盘、鼠标、游戏杆、打印机、扫描仪、存储设备、调制解调器和视频会议摄像机之类的外设提供标准的低成本连接。 对于所有使用旧端口（例如 PS/2 端口、串行端口和并行端口）的外围设备，建议迁移到 USB。

USB-IF 是一个特别兴趣组 (SIG)，负责维护[官方 USB 规范](http://www.usb.org/developers/docs/)、测试规范和工具。

Windows 操作系统为 USB 主控制器、集线器以及符合官方 USB 规范的设备和系统提供本机支持。 Windows 还提供编程接口，用于开发可与 USB 设备通信的[设备驱动程序](usb-driver-development-guide.md)和[应用程序](developing-windows-applications-that-communicate-with-a-usb-device.md)。

[![usb 设备生成器](images/icon-dev.png)](building-usb-devices-for-windows.md)[![面向驱动程序开发人员的 usb](images/icon-driver.png)](usb-driver-development-guide.md)[![面向应用开发人员的 usb](images/icon-app.png)](developing-windows-applications-that-communicate-with-a-usb-device.md)[![usb hck 认证](images/icon-cert.png)](windows-hardware-certification-kit-tests-for-usb.md)

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Windows 中的 USB</strong>
<p></p>
<a href="windows-10--what-s-new-for-usb.md" data-raw-source="[Windows 10: What's new for USB](windows-10--what-s-new-for-usb.md)">Windows 10：USB 的新增功能</a>
<p>概述 Windows 10 中 USB 的新功能和改进。</p>
<a href="usb-faq--introductory-level.md" data-raw-source="[USB FAQ](usb-faq--introductory-level.md)">USB 常见问题解答</a>
<p>驱动程序开发人员提出的在 USB 中受支持的 USB 堆栈和功能的常见问题。</p>
<a href="microsoft-defined-usb-descriptors.md" data-raw-source="[Microsoft OS Descriptors for USB Devices](microsoft-defined-usb-descriptors.md)">针对 USB 设备的 Microsoft OS 描述符</a>
<p>Windows 定义 MS OS 描述符，在连接到运行 Windows 操作系统的系统时，可以通过这些描述符进行更好的枚举</p>
<strong>Microsoft 提供的 USB 驱动程序</strong>
<p></p>
<a href="usb-device-side-drivers-in-windows.md" data-raw-source="[USB device-side drivers in Windows](usb-device-side-drivers-in-windows.md)">Windows 中的 USB 设备端驱动程序</a>
<p>一组驱动程序，用于处理 USB 设备的常见函数逻辑。</p>
<a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers in Windows](usb-3-0-driver-stack-architecture.md)">Windows 中的 USB 宿主端驱动程序</a>
<p>Microsoft 提供驱动程序的核心堆栈，这些驱动程序可以与连接到 EHCI 和 xHCI 控制器的设备互操作。</p>
<a href="supported-usb-classes.md" data-raw-source="[USB-IF device class drivers](supported-usb-classes.md)">USB-IF 设备类驱动程序</a>
<p>Windows 为许多经 USB-IF 批准的设备类、音频、大容量存储等提供随机设备类驱动程序。</p>
<a href="winusb.md" data-raw-source="[USB generic function driver–WinUSB](winusb.md)">USB 常规功能驱动程序 – WinUSB</a>
<p>Windows 提供的 Winusb.sys 可以作为自定义设备的功能驱动程序加载，以及作为复合设备的函数加载。</p>
<a href="usb-common-class-generic-parent-driver.md" data-raw-source="[USB generic parent driver for composite devices–Usbccgp](usb-common-class-generic-parent-driver.md)">适用于复合设备的 USB 常规父驱动程序 – Usbccgp</a>
<p>多功能 USB 设备的父驱动程序。 Usbccgp 为每个这样的功能创建物理设备对象 (PDO)。 这些单独的 PDO 由各自的 USB 功能驱动程序管理，这些驱动程序可以是 Winusb.sys 驱动程序，也可以是 USB 设备类驱动程序。</p>
<strong>适用于开发 USB 驱动程序的 WDF 扩展</strong>
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/mt188011" data-raw-source="[USB connector manager class extension (UcmCx)](https://msdn.microsoft.com/library/windows/hardware/mt188011)">USB 连接器管理器类扩展 (UcmCx)</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/mt188009" data-raw-source="[USB host controller extension (UCX) reference](https://msdn.microsoft.com/library/windows/hardware/mt188009)">USB 主控制器扩展 (UCX) 参考</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/mt188013" data-raw-source="[USB function class extension (UFX) reference](https://msdn.microsoft.com/library/windows/hardware/mt188013)">USB 函数类扩展 (UFX) 参考</a></li>
</ul>
<strong>通过 Windows 测试 USB 设备</strong>
<p></p>
<a href="usb-driver-testing-guide.md" data-raw-source="[Testing USB hardware, drivers, and apps in Windows](usb-driver-testing-guide.md)">在 Windows 中测试 USB 硬件、驱动程序和应用程序</a>
<p>获取相关工具的信息，这些工具可以用来测试 USB 硬件或软件、捕获操作和其他系统事件的跟踪，以及观察 USB 驱动程序堆栈如何响应客户端驱动程序或应用程序发送的请求。</p>
<p>阅读硬件认证工具包中提供的测试的概述。硬件供应商和设备制造商可以通过这些测试准备其 USB 设备和主控制器，以便提交 Windows 硬件认证。</p>
<p><strong>USB 的其他资源</strong></p>
<a href="http://www.usb.org/developers/docs/" data-raw-source="[Official USB Specification](http://www.usb.org/developers/docs/)">官方 USB 规范</a>
<p>针对 USB 协议提供完整的技术详细信息。</p>
<a href="http://blogs.msdn.com/b/usbcoreblog/" data-raw-source="[Microsoft Windows USB Core Team Blog](http://blogs.msdn.com/b/usbcoreblog/)">Microsoft Windows USB 核心团队博客</a>
<p>查看 Microsoft USB 团队撰写的博文。 此博客重点介绍 Windows USB 驱动程序堆栈，该堆栈适用于 Windows 电脑中的各种 USB 主控制器和 USB 集线器。 适用于 USB 客户端驱动程序开发人员和 USB 硬件设计人员的资源，方便他们了解驱动程序堆栈实现、解决常见问题以及如何使用工具来收集跟踪和日志文件。</p>
<a href="http://www.osronline.com/cf.cfm?PageURL=showlists.cfm?list=NTDEV" data-raw-source="[OSR Online Lists - ntdev](http://www.osronline.com/cf.cfm?PageURL=showlists.cfm?list=NTDEV)">OSR Online 列表 - ntdev</a>
<p>由 <a href="http://www.osronline.com/index.cfm" data-raw-source="[OSR Online](http://www.osronline.com/index.cfm)">OSR Online</a> 管理的讨论列表，适用于内核模式驱动程序开发人员。</p>
<a href="https://msdn.microsoft.com/windows/hardware/" data-raw-source="[Windows Dev-Center for Hardware Development](https://msdn.microsoft.com/windows/hardware/)">专注硬件开发的 Windows 开发人员中心</a>
<p>各种基于常见问题的资源，这些问题由不熟悉 Windows 操作系统的 USB 设备和驱动程序开发的开发人员提出。</p>
<p></p>
<p><strong>USB 相关视频</strong></p>
<a href="http://channel9.msdn.com/Events/Build/2013/3-924a" data-raw-source="[UWP apps for USB devices](http://channel9.msdn.com/Events/Build/2013/3-924a)">用于 USB 设备的 UWP 应用</a>
<a href="http://channel9.msdn.com/events/BUILD/BUILD2011/HW-256T" data-raw-source="[Understanding USB 3.0 in Windows 8](http://channel9.msdn.com/events/BUILD/BUILD2011/HW-256T)">了解 Windows 8 中的 USB 3.0</a>
<a href="http://channel9.msdn.com/events/BUILD/BUILD2011/HW-773T" data-raw-source="[Building great USB 3.0 devices](http://channel9.msdn.com/events/BUILD/BUILD2011/HW-773T)">构建卓越的 USB 3.0 设备</a>
<a href="http://channel9.msdn.com/events/BUILD/BUILD2011/HW-258P" data-raw-source="[USB Debugging Innovations in Windows 8 (Part I, II, &amp; III)](http://channel9.msdn.com/events/BUILD/BUILD2011/HW-258P)">Windows 8 中的 USB 调试创新（第 1、第 2 和第 3 部分）</a>
<p><strong>适合学习的 USB 硬件</strong></p>
<a href="microsoft-usb-test-tool--mutt--devices.md" data-raw-source="[MUTT devices](microsoft-usb-test-tool--mutt--devices.md)">MUTT 设备</a>
<p>MUTT 和 SuperMUTT 设备以及伴随的软件包已集成到包含 USB 测试的 HCK 套件中。 它们提供的自动化测试可以在 USB 控制器、设备和系统的开发周期中使用，尤其是在进行压力测试时使用。</p>
<a href="http://www.osronline.com/index.cfm" data-raw-source="[OSR USB FX2 Learning Kit](http://www.osronline.com/index.cfm)">OSR USB FX2 学习工具包</a>
<p>前提是你不熟悉 USB 驱动程序开发。 此工具包最适合学习本文档集中包括的 USB 示例。 可以从 OSR Online 商店获取学习工具包。</p></td>
<td><strong>编写 USB 客户端驱动程序（KMDF、UMDF）</strong>
<p>USB 驱动程序开发简介。 介绍在为设备提供 USB 驱动程序时如何选择最适合的模型。 此部分还包括一些教程，介绍如何使用 Microsoft Visual Studio 随附的 USB 模板编写第一个用户模式的 USB 驱动程序和内核模式的 USB 驱动程序。</p>
<p><a href="getting-started-with-usb-client-driver-development.md" data-raw-source="[Getting started with USB client driver development](getting-started-with-usb-client-driver-development.md)">USB 客户端驱动程序开发入门</a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540134" data-raw-source="[USB device driver programming reference](https://msdn.microsoft.com/library/windows/hardware/ff540134)">USB device driver programming reference</a>（USB 设备驱动程序编程参考）</p>
<strong>编写 USB 主控制器驱动程序</strong>
<p>如果开发不符合规格的 xHCI 主控制器，或者开发自定义的非 xHCI 硬件（例如虚拟主控制器），则可编写可以与 UCX 通信的主控制器驱动程序。 例如，可以考虑支持 USB 设备的无线坞。 电脑通过无线坞与 USB 设备通信，使用基于 TCP 的 USB 作为传输方式。</p>
<p><a href="developing-windows-drivers-for-usb-host-controllers.md" data-raw-source="[Developing Windows drivers for USB host controllers](developing-windows-drivers-for-usb-host-controllers.md)">为 USB 主控制器开发 Windows 驱动程序</a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt188009" data-raw-source="[USB host controller driver programming reference](https://msdn.microsoft.com/library/windows/hardware/mt188009)">USB host controller driver programming reference</a>（USB 主控制器驱动程序编程参考）</p>
<strong>为 USB 设备编写功能控制器驱动程序</strong>
<p>可以开发控制器驱动程序，用于处理由主机发送到设备的所有 USB 数据传输内容和命令。 此驱动程序可以与 Microsoft 提供的 USB 功能控制器扩展 (UFX) 通信。</p>
<p><a href="developing-windows-drivers-for-usb-function-controllers.md" data-raw-source="[Developing Windows drivers for USB function controllers](developing-windows-drivers-for-usb-function-controllers.md)">为 USB 功能控制器开发 Windows 驱动程序</a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt188013" data-raw-source="[USB function controller programming reference](https://msdn.microsoft.com/library/windows/hardware/mt188013)">USB function controller programming reference</a>（USB 功能控制器编程参考）</p>
<strong>编写 USB 类型 C 连接器驱动程序</strong>
<p>Windows 10 引入了对新 USB 连接器：USB 类型 C 的支持。 可以为连接器编写驱动程序，以便与 Microsoft 提供的类扩展模块UcmCx 通信，以便处理与类型 C 连接器相关的场景，例如，哪些端口支持类型 C、哪些端口支持功率输出。</p>
<p><a href="developing-windows-drivers-for-usb-type-c-connectors.md" data-raw-source="[Developing Windows drivers for USB Type-C connectors](developing-windows-drivers-for-usb-type-c-connectors.md)">为 USB 类型 C 连接器开发 Windows 驱动程序</a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt188011" data-raw-source="[USB connector manager class extension (UcmCx) reference](https://msdn.microsoft.com/library/windows/hardware/mt188011)">USB 连接器管理器类扩展 (UcmCx) 参考</a></p>
<strong>编写 USB 双角色控制器驱动程序</strong>
<p>Windows 10 现在支持 USB 双角色控制器。 Windows 包括的随机客户端驱动程序适用于 ChipIdea 和 Synopsys 控制器。 对于其他控制器，Microsoft 提供一组编程接口，方便双角色类扩展 (UrsCx) 及其客户端驱动程序互相通信，从而处理双角色控制器的角色切换功能。</p>
<p>有关此功能的详细信息，请参阅：</p>
<p><a href="usb-dual-role-driver-stack-architecture.md" data-raw-source="[USB Dual Role Driver Stack Architecture](usb-dual-role-driver-stack-architecture.md)">USB 双角色驱动程序堆栈体系结构</a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt628026" data-raw-source="[USB dual-role controller driver programming reference](https://msdn.microsoft.com/library/windows/hardware/mt628026)">USB dual-role controller driver programming reference</a>（USB 双角色控制器驱动程序编程参考）</p>
<strong>编写用于模拟设备的 USB 驱动程序</strong>
<p>Windows 10 引入了对模拟设备的支持。 现在可以开发模拟通用串行总线 (USB) 主控制器驱动程序和连接的虚拟 USB 设备。 这两个组件组合成单个 KMDF 驱动程序，该驱动程序可以与 Microsoft 提供的 USB 设备模拟类扩展 (UdeCx) 通信。</p>
<p><a href="developing-windows-drivers-for-emulated-usb-host-controllers-and-devices.md" data-raw-source="[Developing Windows drivers for emulated USB devices (UDE)](developing-windows-drivers-for-emulated-usb-host-controllers-and-devices.md)">开发模拟 USB 设备 (UDE) 的 Windows 驱动程序</a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt628025" data-raw-source="[Emulated USB host controller driver programming reference](https://msdn.microsoft.com/library/windows/hardware/mt628025)">Emulated USB host controller driver programming reference</a>（模拟 USB 主控制器驱动程序编程参考）</p>
<strong>编写 UWP 应用</strong>
<p>提供如何在 UWP 应用中实现 USB 功能的分步说明。 若要为 USB 设备编写此类应用，需要使用 Visual Studio 和 Microsoft Windows 软件开发工具包 (SDK)。</p>
<p><a href="talking-to-usb-devices-start-to-finish.md" data-raw-source="[Talk to USB devices, start to finish](talking-to-usb-devices-start-to-finish.md)">与 USB 设备通信，从开始到完成</a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb" data-raw-source="[&lt;strong&gt;Windows.Devices.Usb&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)"><strong>Windows.Devices.Usb</strong></a></p>
<strong>编写 Windows 桌面应用</strong>
<p>介绍应用程序如何通过调用 WinUSB 函数与 USB 设备通信。</p>
<p><a href="how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md" data-raw-source="[Write a WinUSB application](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)">编写 WinUSB 应用程序</a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb" data-raw-source="[&lt;strong&gt;WinUSB Functions&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)"><strong>WinUSB 函数</strong></a></p>
<a href="wdk-resources-for-usb-driver-development.md" data-raw-source="[Common programming scenarios](wdk-resources-for-usb-driver-development.md)">常见编程方案</a>
<p>列出了驱动程序或应用在与 USB 设备通信时需执行的常见任务。 快速了解每个任务所需的编程接口。</p>
<p></p>
<p><strong>USB 示例</strong></p>
<p><a href="https://go.microsoft.com/fwlink/p/?LinkID=309716" data-raw-source="[UWP app samples for USB](https://go.microsoft.com/fwlink/p/?LinkID=309716)">USB 的 UWP 应用示例</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=618021" data-raw-source="[Windows driver samples for USB](https://go.microsoft.com/fwlink/p/?linkid=618021)">USB 的 Windows 驱动程序示例</a></p>
<p><strong>开发工具</strong></p>
<a href="https://go.microsoft.com/fwlink/p/?linkid=619491" data-raw-source="[Download kits and tools for Windows]( https://go.microsoft.com/fwlink/p/?linkid=619491)">下载适用于 Windows 的工具包和工具</a></td>
</tr>
</tbody>
</table>

 

 

 




