---
description: 重点介绍 Windows 10 中通用串行总线 (USB) 的新增功能和改进。
title: Windows 10-USB 的新增功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcef817cd664d3237011e9b315b72e3192fef239
ms.sourcegitcommit: 46b8f226ad7fff5ee742007ce6525d0440482034
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2020
ms.locfileid: "97486460"
---
# <a name="windows-10-whats-new-for-usb"></a>Windows 10：USB 的新增功能


本主题重点介绍 Windows 10 中的通用串行总线 (USB) 的新增功能和改进。

-  **UCSI 驱动程序扩展** 从 Windows 10 1809 版开始，添加了一个适用于 UCSI ( # A0) 的新类扩展，该扩展以与传输无关的方式实现 UCSI 规范。 只需编写极少量的代码，驱动程序（即 UcmUcsiCx 的客户端）即可通过非 ACPI 传输来与 USB 类型 C 硬件通信。 本主题介绍 UCSI 类扩展提供的服务，以及客户端驱动程序的预期行为。

-   **USB 类型-C 端口控制器接口** 

    Windows 10 版本1703提供 ( # A0) 的类扩展，该扩展插件支持通用串行总线类型 C 端口控制器接口规范。 USB 类型 C 连接器驱动程序不需要保留任何内部的 PD/类型 C 状态。 
    管理 USB C 型连接器和 USB 电源输送 (PD) 状态机时存在的复杂性由系统处理。 你只需编写一个客户端驱动程序，以便通过该类扩展将硬件事件传送给系统即可。 

    [USB 类型 C 端口控制器接口驱动程序类扩展参考](/previous-versions/windows/hardware/drivers/mt805826(v=vs.85))

-   **USB 双重角色支持。**

    Windows 中现在支持 USB 双重角色控制器。 Windows 包括的随机客户端驱动程序适用于 ChipIdea 和 Synopsys 控制器。 对于其他控制器，Microsoft 提供一组编程接口，方便双角色类扩展 (UrsCx) 及其客户端驱动程序互相通信，从而处理双角色控制器的角色切换功能。

    有关此功能的详细信息，请参阅：

    [USB 双角色驱动程序堆栈体系结构](usb-dual-role-driver-stack-architecture.md)

    [USB 双角色控制器驱动程序编程参考](/previous-versions/windows/hardware/drivers/mt628026(v=vs.85))

-   **用于开发 USB 类型 C 连接器驱动程序的一组新的编程接口。**

    此版本引入了对 usb 3.1 规范中定义的 USB 类型 C 的本机支持。 此功能可让设备使用可逆连接器、对称电缆、更快的充电和通过 USB 电缆运行的备用模式。 通过这些编程接口，您可以在本部分中为连接器 (称为客户端驱动程序的驱动程序) 与 Microsoft 提供的类扩展模块通信： UcmCx 来处理与类型 C 连接器相关的方案，例如，哪些端口支持类型 C，哪些端口支持电源传送。

    [为 USB 类型 C 连接器开发 Windows 驱动程序](developing-windows-drivers-for-usb-type-c-connectors.md)

    [USB 连接器管理器类扩展 (UcmCx)](/previous-versions/windows/hardware/drivers/mt188011(v=vs.85))

-   **用于开发模拟主机控制器和连接的虚拟设备的一组新的编程接口。**

    Windows 10 引入了对模拟设备的支持。 现在可以开发模拟通用串行总线 (USB) 主控制器驱动程序和连接的虚拟 USB 设备。 这两个组件组合成单个 KMDF 驱动程序，该驱动程序可以与 Microsoft 提供的 USB 设备模拟类扩展 (UdeCx) 通信。

    [开发模拟 USB 设备 (UDE) 的 Windows 驱动程序](developing-windows-drivers-for-emulated-usb-host-controllers-and-devices.md)

    [模拟 USB 主控制器驱动程序编程参考](/previous-versions/windows/hardware/drivers/mt628025(v=vs.85))

-   **用于开发 USB 主机控制器驱动程序的一组新的编程接口。**

    如果你的硬件不符合规范 xHCI 或正在写入虚拟主机控制器，则可以开发主机控制器，如通过 TCP 连接将 USB 流量路由到连接到设备的外围设备的控制器。 主机控制器驱动程序是 USB 主机控制器扩展的客户端，它是一个遵循框架类扩展模型的系统提供的驱动程序。 在 [MICROSOFT USB 3.0 驱动程序堆栈](/windows-hardware/drivers/ddi/index#usb-3-0-driver-stack)中，UCX 提供了帮助主机控制器驱动程序管理 USB 主机控制器设备的功能。

    [为 USB 主控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-host-controllers.md)

    [USB 主控制器扩展 (UCX) 参考](/previous-versions/windows/hardware/drivers/mt188009(v=vs.85))

-   **用于开发 USB 函数控制器驱动程序的一组新的编程接口。**

    可以编写一个客户端驱动程序，该驱动程序与 USB 函数类扩展 (UFX) 并实现控制器特定的操作。 UFX 处理所有 USB 函数控制器通用的 USB 函数逻辑。

    [Windows 中的 USB 设备端驱动程序](usb-device-side-drivers-in-windows.md)

    [USB 功能客户端驱动程序使用的 UFX 对象和句柄](ufx-objects-and-handles-used-by-a-usb-function-controller.md)

    [函数控制器客户端驱动程序的任务](function-client-driver.md)

    [UFX 编程参考的用户模式服务](/windows-hardware/drivers/ddi/ufxclient)

    [UFX 编程参考的 USB 函数类驱动程序](/previous-versions/windows/hardware/drivers/mt188008(v=vs.85))

    [USB 函数控制器客户端驱动程序编程参考](/previous-versions/windows/hardware/drivers/mt188010(v=vs.85))

    [用于支持专用充电器的 USB 筛选器驱动程序](/previous-versions/windows/hardware/drivers/mt188012(v=vs.85))

-   **提高了 USB CDC (串行) 设备的体验。**

    使用 Usbser.sys 驱动程序，允许与 USB 通信设备类兼容的设备 (类 \_ 02 & 子类 \_ 02) 使用 Windows 10。 不再需要设备制造商编写自定义 INF 即可安装该驱动程序。

    [USB 串行驱动程序 (Usbser.sys)](usb-driver-installation-based-on-compatible-ids.md)

 

