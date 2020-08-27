---
description: 介绍 USB 类型 C 系统和 Microsoft 提供的支持硬件组件的驱动程序的典型硬件设计。
title: 适用于 Windows 系统的 USB 类型 C 设计体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65bd0dfc6001bc380cc7f8b8187878edf57f9833
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969024"
---
# <a name="architecture-usb-type-c-design-for-a-windows-system"></a>体系结构：Windows 系统的 USB 类型 C 设计


**适用于通过 USB 类型 C 连接器开发系统的 Oem**

-   使用 USB 类型的 USB 双重角色功能-C
-   使用 USB 类型-C 当前级别和电源交付2.0 提高了充电速度
-   使用备用模式和有线插接体验的显示功能。

**上次更新时间**

-   2016 年 12 月

**Windows 版本**

-   Windows 10 桌面版（家庭版、专业版、企业版和教育版）
-   Windows 10 移动版

介绍 USB 类型 C 系统和 Microsoft 提供的支持硬件组件的驱动程序的典型硬件设计。

## <a name="drivers-for-supporting-usb-type-c-components"></a><a href="" id="drivers"></a>支持 USB 类型 C 组件的驱动程序


![USB 类型 C 软件组件](images/type-c-arch.png)

在上图中，

-   **USB 设备端驱动程序**

    [USB 设备端驱动程序](usb-device-side-drivers-in-windows.md)为功能/设备/外设提供服务。 USB 功能控制器类扩展支持 MTP（媒体传输协议），并使用 BC 1.2 充电器进行充电。 Microsoft 为 Synopsys USB 3.0 和 ChipIdea USB 2.0 控制器提供随机客户端驱动程序。 可以通过使用 [USB 功能控制器客户端驱动程序编程接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188010(v=vs.85))，为功能控制器编写自定义客户端驱动程序。 有关详细信息，请参阅[为 USB 功能控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-function-controllers.md)。

    SoC 供应商可能会向你提供 USB 函数的更低筛选器驱动程序，以便进行传统的专用充电器检测。 如果函数控制器为 Synopsys USB 3.0 或 ChipIdea USB 2.0 控制器，则可以实现自己的筛选器驱动程序

-   **USB 主机端驱动程序**

    USB 主机端驱动程序是适用于与 EHCI 或 XHCI 兼容的 USB 主机控制器的一组驱动程序。 如果角色切换驱动程序枚举主机角色，则会加载驱动程序。 如果主机控制器不符合规范，则可以使用 [USB 主机控制器扩展 (UCX) 编程接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188009(v=vs.85))来写入自定义驱动程序。 有关信息，请参阅[为 USB 主机控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-host-controllers.md)。

    请注意，    并非[所有 USB 设备类](supported-usb-classes.md)在 Windows 10 移动版上都受支持。

     

-   **USB 角色-交换机驱动程序 (URS) **

    系统可设计为双重角色 USB 端口需要 Windows 将其配置为主机或函数模式。 这些设计需要使用 USB 角色开关 (URS) 驱动程序堆栈。

    URS 驱动程序管理连接器、主机或功能的当前角色，以及根据平台中的硬件事件加载和卸载适当的设备端或主机端驱动程序。 Microsoft 为 Synopsys USB 3.0 和 ChipIdea USB 2.0 控制器提供随机客户端驱动程序。 可以使用 [USB 双重角色控制器驱动程序编程接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt628026(v=vs.85))编写角色切换客户端驱动程序。 若要激活角色切换驱动程序，必须对 ACPI 表进行更改。 有关详细信息，请参阅 [USB 双重角色驱动程序堆栈体系结构](usb-dual-role-driver-stack-architecture.md)。

    在带有 USB 微 AB 连接器的系统上，此决定是根据连接器中的 ID pin 来决定的。 ID pin 检测由客户端驱动程序通过使用分配给它的中断资源来执行。

    在带有 USB 类型 C 连接器的系统上，将根据 CC pin 来做出决定。 连接器的客户端驱动程序执行 CC 检测并将该信息转发到角色切换驱动程序。

-   **USB 连接器管理器 (UCM) **

    这组驱动程序管理 USB 类型 C 连接器的所有方面。 如果系统通过 ACPI 实现 UCSI 兼容的嵌入式控制器，请使用 Microsoft 提供的 [UCSI 驱动程序](ucsi.md)。 否则，请为非 ACPI 传输 [编写 UCSI 客户端驱动程序](write-a-ucsi-driver.md) 。

    如果你的硬件不是 UCSI 兼容的，则应将作为客户端的 [USB 类型 C 连接器驱动程序写入](bring-up-a-usb-type-c-connector-on-a-windows-system.md) UCM 类扩展。 它们共同管理 USB 类型 C 连接器和连接器驱动程序的预期行为。

    如果你正在编写驱动程序，则 USB 连接器管理器类扩展将遵循 WDF 类扩展-客户端驱动程序模型。 你的客户端驱动程序与硬件和类扩展通信，以处理诸如 CC 检测、PD 消息传递、Muxing 和 VBus/VConn 控件等任务，并为电源传递和备用模式选择策略。 类扩展将客户端驱动程序报告的信息传递给操作系统。 例如，CC 检测结果用于配置角色切换驱动程序;USB 类型-C/PD 电源信息用于确定系统应收取的费用。 客户端驱动程序管理 USB 类型 C 和 PD 状态机。 客户端驱动程序可以将一些任务委托给其他驱动程序，例如 Mux 可能由另一个驱动程序控制。 若要编写客户端驱动程序，请使用 [USB 类型 C 连接器驱动程序编程接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188011(v=vs.85))。

    **USB 类型-C 端口控制器**

    C # A0) 的类型 C 端口控制器接口类扩展 ( 是 Microsoft 提供的 USB 连接器管理器的扩展，它允许操作系统在不实现 PD 状态的连接器 (TCPM) 。 UcmTcpciCx 客户端驱动程序允许软件 TCPM 控制硬件并实时获取其状态。

    有关编写客户端驱动程序的信息，请参阅 [编写 USB 类型 C 端口控制器驱动程序](write-a-usb-type-c-port-controller-driver.md)。

-   **充电仲裁驱动程序**

    此驱动程序由 Microsoft 提供，适用于 Windows 10 移动版。 驱动程序充当多个充电源的仲裁器。 USB 连接器管理器会报告 USB 类型 C 和 PD 向 CAD 收费的源信息，这会从该信息进行选择，并通过 USB 设备端驱动程序执行的 BC 1.2 充电器检测 (（如果适用) ）。 然后，CAD 会报告用于电池子系统的最合适的充电来源。

-   **电池驱动程序**

    类驱动程序定义系统中电池的整体功能，并与电源管理器进行交互。 Miniclass 驱动程序处理特定于设备的功能，例如添加和取出电池，并跟踪其容量和电量。 Miniclass 驱动程序导出类驱动程序调用的例程，以获取有关它所控制设备的信息。

 

 




