---
Description: Highlights the new features and improvements for Universal Serial Bus (USB) in Windows 10.
title: Windows 10-什么是 USB 的新增功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f319c777e662059ee146d02321d15b73e11b2fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540454"
---
# <a name="windows-10-whats-new-for-usb"></a>Windows 10：什么是 USB 的新增功能


本主题重点介绍新功能和改进的通用串行总线 (USB) 在 Windows 10。

-  **UCSI 驱动程序扩展**从 Windows 10，版本 1809，开始 UCSI (UcmUcsiCx.sys) 的新类扩展已添加，它在传输过程中实现 UCSI 规范无关的方式。 使用极少量的代码，您的驱动程序，这是到 UcmUcsiCx 的客户端，都可与 USB 类型 C 硬件通过非 ACPI 传输通信。 本主题介绍提供 UCSI 类扩展和客户端驱动程序的预期的行为的服务。

-   **USB 类型 C 端口控制器接口** 

    Windows 10 1703年版提供了支持通用串行总线类型 C 端口控制器接口规范的类扩展插件 (UcmTcpciCx.sys)。 USB 类型 C 连接器驱动程序不需要维护任何内部 PD/类型-C 状态。 
    由系统处理的管理的 USB C 型连接器和 USB Power 传递 (PD) 状态机。 只需编写通信通过此类扩展系统的硬件事件的客户端驱动程序。 

    [USB 类型 C 端口控制器界面驱动程序类扩展参考](https://msdn.microsoft.com/library/windows/hardware/mt805826)

-   **USB 双角色支持。**

    在 Windows 中现在支持 USB 双角色控制器。 Windows 包含 ChipIdea 和 Synopsys 控制器的内置客户端驱动程序。 对于其他控制器，Microsoft 提供了一组允许进行双角色类扩展 (UrsCx) 和其客户端驱动程序进行通信与其他处理双角色控制器的角色切换功能的编程接口。

    有关此功能的详细信息，请参阅：

    [USB 双角色驱动程序堆栈体系结构](usb-dual-role-driver-stack-architecture.md)

    [编程参考的 USB 双角色控制器驱动程序](https://msdn.microsoft.com/library/windows/hardware/mt628026)

-   **新组用于开发 USB 类型 C 连接器驱动程序的编程接口。**

    此版本引入了本机支持 USB 类型-C，USB 3.1 规范中定义。 该功能允许设备使用可逆连接器、 更快地收费，对称电缆和 USB 电缆通过运行的其他模式。 这些编程接口使您得以编写适用于与 Microsoft 提供的类扩展模块进行通信的连接器 （在本部分中称为客户端驱动程序） 的驱动程序：UcmCx 来处理方案，与相关类型 C 连接器如，哪些端口支持类型-C，端口 power 提供支持。

    [开发 USB 类型 C 连接器的 Windows 驱动程序](developing-windows-drivers-for-usb-type-c-connectors.md)

    [USB 连接器管理器类扩展 (UcmCx)](https://msdn.microsoft.com/library/windows/hardware/mt188011)

-   **新组用于开发仿真的主机控制器和连接的虚拟设备的编程接口。**

    Windows 10 引入了对模拟设备的支持。 现在可以开发模拟通用串行总线 (USB) 主机控制器驱动程序和连接的虚拟 USB 设备。 这两个组件组合成单个 KMDF 驱动程序由 Microsoft 提供的 USB 设备仿真类扩展 (UdeCx) 与之通信。

    [开发模拟 USB 设备 (UDE) 的 Windows 驱动程序](developing-windows-drivers-for-emulated-usb-host-controllers-and-devices.md)

    [模拟的 USB 主机控制器驱动程序的编程参考](https://msdn.microsoft.com/library/windows/hardware/mt628025)

-   **新组用于开发 USB 主控制器驱动程序的编程接口。**

    如果您的硬件不符合规范的 xHCI，或者你可以开发主机控制器编写一个虚拟主机控制器，如将 USB 流量路由通过 TCP 连接到外围设备的控制器附加到设备。 主机控制器驱动程序是 USB 主机控制器扩展，这是遵循 framework 类扩展模型的系统提供驱动程序的客户端。 内[Microsoft USB 3.0 驱动程序堆栈](https://msdn.microsoft.com/library/windows/hardware/hh406256.aspx#usb-3-0-driver-stack)，UCX 提供功能以帮助在主机中管理 USB 主机控制器设备控制器驱动程序。

    [开发 USB 主控制器的 Windows 驱动程序](developing-windows-drivers-for-usb-host-controllers.md)

    [USB 主机控制器扩展 (UCX) 参考](https://msdn.microsoft.com/library/windows/hardware/mt188009)

-   **新组用于开发 USB 函数控制器驱动程序的编程接口。**

    您可以编写与 USB 函数类扩展 (UFX) 进行通信并实现特定于控制器的操作的客户端驱动程序。 UFX 处理普遍适用于所有 USB 函数控制器的 USB 函数逻辑。

    [在 Windows 中的 USB 设备端驱动程序](usb-device-side-drivers-in-windows.md)

    [UFX 对象和 USB 函数客户端驱动程序使用的句柄](ufx-objects-and-handles-used-by-a-usb-function-controller.md)

    [函数的控制器客户端驱动程序任务](function-client-driver.md)

    [用户模式服务添加到 UFX 编程参考](https://msdn.microsoft.com/library/windows/hardware/mt188014)

    [USB 到 UFX 编程参考的函数类驱动程序](https://msdn.microsoft.com/library/windows/hardware/mt188008)

    [USB 函数控制器客户端驱动程序编程参考](https://msdn.microsoft.com/library/windows/hardware/mt188010)

    [支持专有充电器 USB 筛选器驱动程序](https://msdn.microsoft.com/library/windows/hardware/mt188012)

-   **改进了 USB CDC （串行） 设备的体验。**

    允许使用 USB 通信设备类合规的设备 (类\_02 和子类\_02) 以使用 Windows 10 使用 Usbser.sys 驱动程序。 设备制造商不再需要编写自定义 INF 安装该驱动程序。

    [USB 串行驱动程序 (Usbser.sys)](usb-driver-installation-based-on-compatible-ids.md)

 

 




