---
Description: 介绍了典型的硬件设计 USB C 类型系统和支持的硬件组件的 Microsoft 提供驱动程序。
title: Windows 系统的 USB 类型 C 设计的体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8e584929528c85dcb5002dea4dae9abfd3ba025
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384489"
---
# <a name="architecture-usb-type-c-design-for-a-windows-system"></a>体系结构：Windows 系统的 USB 类型 C 设计


**适用于开发与 USB 类型 C 连接器的系统的 Oem**

-   通过使用 USB 类型 C USB 双角色功能
-   通过使用 USB 类型 C 当前级别和 Power 交付 2.0 更快地收费
-   显示扩展功能，通过使用备用模式和有线停靠的体验。

**上次更新时间**

-   2016 年 12 月

**Windows 版本**

-   Windows 10 桌面版（家庭版、专业版、企业版和教育版）
-   Windows 10 移动版

介绍了典型的硬件设计 USB C 类型系统和支持的硬件组件的 Microsoft 提供驱动程序。

## <a href="" id="drivers"></a>支持 USB 类型 C 组件的驱动程序


![usb 类型 c 软件组件](images/type-c-arch.png)

在上图中，

-   **USB 设备端驱动程序**

    [USB 设备端驱动程序](usb-device-side-drivers-in-windows.md)服务函数/设备/外设。 USB 函数控制器类扩展支持 MTP （媒体传输协议） 和充电使用 BC 1.2 充电器。 Microsoft 为 Synopsys USB 3.0 和 ChipIdea USB 2.0 控制器提供内置客户端驱动程序。 你可以通过使用为函数控制器编写自定义客户端驱动程序[USB 函数控制器客户端驱动程序的编程接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188010(v=vs.85))。 有关详细信息，请参阅[开发的 Windows USB 驱动程序函数控制器](developing-windows-drivers-for-usb-function-controllers.md)。

    SoC 供应商可能会为您提供 USB 函数较低筛选器驱动程序的旧专有充电器检测。 如果函数控制器是 Synopsys USB 3.0 或 ChipIdea USB 2.0 控制器，则可以实现你自己的筛选器驱动程序

-   **USB 宿主端驱动程序**

    USB 宿主端驱动程序是一组使用 EHCI 或 XHCI 符合 USB 主控制器的驱动程序。 如果在角色切换驱动程序枚举主机角色，将加载的驱动程序。 如果您的主控制器不符合规范，则可以通过编写自定义驱动程序[USB 主机控制器扩展 (UCX) 编程接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188009(v=vs.85))。 有关信息，请参阅[开发的 Windows USB 驱动程序托管控制器](developing-windows-drivers-for-usb-host-controllers.md)。

    **请注意**  不[USB 设备的所有类](supported-usb-classes.md)在 Windows 10 移动版上受支持。

     

-   **USB 角色切换驱动程序 (URS)**

    可以设计系统，以便双角色 USB 端口需要 Windows 配置为主机或函数的模式。 这些设计将需要使用 USB 角色切换 (URS) 驱动程序堆栈。

    URS 驱动程序管理连接器、 主机或函数和加载的当前角色和卸载的适当的设备端或主机端驱动程序，基于硬件的平台的事件。 Microsoft 为 Synopsys USB 3.0 和 ChipIdea USB 2.0 控制器提供内置客户端驱动程序。 您可以通过编写在角色切换客户端驱动程序[USB 双角色控制器驱动程序的编程接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt628026(v=vs.85))。 若要激活的角色切换驱动程序，必须对 ACPI 表进行更改。 有关详细信息，请参阅[USB 双角色驱动程序堆栈体系结构](usb-dual-role-driver-stack-architecture.md)。

    在系统上使用 USB 微 AB 连接器，此决定基于的连接器中的 ID 插针。 由客户端驱动程序通过使用分配给它的中断资源来执行 ID pin 检测。

    在系统上使用 USB 类型 C 连接器，做出的决定是基于抄送插针上。 连接器的客户端驱动程序执行抄送检测并将转发到角色切换驱动程序的信息。

-   **USB 连接器管理器 (UCM)**

    本系列驱动程序管理 USB 类型 C 连接器的所有的方面。 如果您的系统通过 ACPI 实现 UCSI 符合嵌入式的控制器，使用 Microsoft 提供[UCSI 驱动程序](ucsi.md)。 否则为[编写 UCSI 客户端驱动程序](write-a-ucsi-driver.md)对于非 ACPI 传输。

    如果您的硬件不 UCSI 兼容的则你应该向[写入 USB 类型 C 连接器驱动程序](bring-up-a-usb-type-c-connector-on-a-windows-system.md)，它是客户端到 UCM 类扩展。 它们一起管理 USB 类型 C 连接器和连接器驱动程序的预期的行为。

    如果你正在编写一个驱动程序，USB 连接器管理器类扩展遵循 WDF 类扩展客户端驱动程序模型。 客户端驱动程序与硬件和类扩展以处理任务，例如抄送检测，消息传送，Muxing，PD 进行通信和 VBus/VConn 控件和 power 交付和备用模式选择策略。 类扩展通信向操作系统报告的客户端驱动程序的信息。 例如，使用抄送检测结果来配置角色切换驱动程序;USB 类型-C/PD 电源信息用于确定系统应收取费用的级别。 客户端驱动程序管理 USB 类型 C 和 PD 状态机。 客户端驱动程序可以委派给其他驱动程序的一些任务，例如，Mux 可能受另一个驱动程序。 若要编写客户端驱动程序，使用[USB 类型 C 连接器驱动程序的编程接口](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188011(v=vs.85))。

    **USB 类型 C 端口控制器**

    类型 C 端口控制器接口类扩展 (UcmTcpciCx.sys) 是扩展到了 USB 连接器管理器允许 OS 在行为不实现 PD 状态机连接器的类型 C 端口管理器 (TCPM) 为 Microsoft 提供的。 UcmTcpciCx 客户端驱动程序允许软件 TCPM 控制硬件和实时获取其状态。

    有关编写客户端驱动程序的信息，请参阅[写入 USB 类型 C 端口控制器驱动程序](write-a-usb-type-c-port-controller-driver.md)。

-   **收费仲裁驱动程序**

    此驱动程序提供的 Microsoft 的 Windows 10 移动版。 该驱动程序充当多个充电源仲裁器。 USB 连接器管理器报告 USB 类型 C 和 PD 充电的 USB 设备端驱动程序 （如果适用） 执行的信息和 BC1.2 充电器检测到加拿大元、 进行选择的源信息。 然后，CAD 报告要使用到电池子系统的最合适充电源。

-   **电池驱动程序**

    类驱动程序定义系统中电池的整体功能，并与电源管理器进行交互。 Miniclass 驱动程序处理特定于设备的功能，例如添加和删除电池，以及跟踪的其容量和费用。 Miniclass 驱动程序将导出的类驱动程序调用以获取有关它控制的设备的信息的例程。

 

 




