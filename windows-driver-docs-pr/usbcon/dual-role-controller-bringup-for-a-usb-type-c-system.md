---
Description: USB 角色切换驱动程序和其处理双角色控制器的角色切换功能的客户端驱动程序。
title: 为 USB 类型 C Windows 系统启动双角色控制器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0039d54bd03783e346e6edad5df23a78e703e3bf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384472"
---
# <a name="bring-up-the-dual-role-controller-for-a-usb-type-c-windows-system"></a>为 USB 类型 C Windows 系统启动双角色控制器


**摘要**

-   OEM 弹出 USB 类型 C 连接器的双角色控制器的任务

**适用于**

-   Windows 10 移动版

**上次更新时间**

-   2016 年 12 月

**重要的 API**

-   [USB dual-role controller driver programming reference](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt628026(v=vs.85))（USB 双角色控制器驱动程序编程参考）

USB 角色切换驱动程序 (URS) 是一套 WDF 类扩展和处理双角色控制器的角色切换功能及其客户端驱动程序。 如果您的系统具有双重角色控制器，则可以切换具体取决于连接到系统的 USB 类型 C 连接器合作伙伴端口设备系统的角色。 这样，如有线停靠感兴趣的情况。

可以设计系统，以便双角色 USB 控制器需要 Windows 配置为主机或函数的模式。 这些设计使用 USB 角色切换堆栈。 如果系统不使用 Synopsys 或 ChipIdea 双角色控制器，你需要为系统的双角色控制器编写 USB 角色切换客户端驱动程序。

**请注意**  系统可设计以便双角色 USB 端口需要 Windows 配置为主机或函数的模式。 这些设计使用 USB 角色切换堆栈。 如果系统不使用 Synopsys 双角色控制器，你需要为系统的双角色控制器编写 USB 角色切换客户端驱动程序。

 

客户端驱动程序处理硬件事件并报告给此类扩展。 如果角色切换硬件事件发生 URS 决定该角色，并因此将加载该角色的驱动程序。 如果控制器在主机角色中， [USB 宿主端驱动程序](usb-3-0-driver-stack-architecture.md)加载; 对于函数角色[设备端驱动程序](usb-device-side-drivers-in-windows.md)加载。

在系统上使用 USB 微 AB 连接器，双角色控制器的客户端驱动程序来作出决定的连接器中的 ID 插针使用分配给它的中断资源。 在系统上使用 USB 类型 C 连接器，此决定是通过连接器的客户端驱动程序。 该驱动程序确定基于抄送角色固定，到了 USB 连接器管理器 (UCM)，后者随后将结果发送到的角色切换驱动程序报告的结果。

![usb 角色切换驱动程序](images/urs.png)

## <a name="1-enable-the-urs-driver-in-system-acpi"></a>1.ACPI 系统中启用 URS 驱动程序


若要使用 URS，必须进行 ACPI 改动。 替换为在其上的设备[USB 设备端驱动程序](usb-device-side-drivers-in-windows.md)URS 必须要加载的设备使用负载均衡。 有关如何更改 ACPI 定义的详细信息，请参阅中提供的示例[USB 双角色驱动程序堆栈体系结构](usb-dual-role-driver-stack-architecture.md)。 请确保删除中断资源。 这不是必需的 USB 类型。

## <a name="2-load-the-usb-role-switch-drivers-for-the-dual-role-controller-driver"></a>2.加载双角色控制器驱动程序的角色切换 USB 驱动程序


![usb 角色切换堆栈](images/urs.png)

-   如果您的系统使用 ChipIdea 和 Synopsys 控制器，加载 Microsoft ChipIdea 和 Synopsys 控制器提供的框中客户端驱动程序。

    若要加载的驱动程序，必须创建一个驱动程序的安装程序包。 INF 文件必须具有**包括需求**指令，它引用的受支持的控制器中框 INF。 在框 INF 已包含的硬件 Id 的其他控制器。 如果双角色控制器的硬件 ID 不是一个现成 INF 中的硬件 Id，则需要此步骤。 请咨询 SoC 供应商。

    详细信息，请参阅"URS 驱动程序包"下[驱动程序安装包](usb-dual-role-driver-stack-architecture.md#inf)。

-   如果您的系统使用自定义控制器，编写在角色切换客户端驱动程序。 有关详细信息，请参阅：

    [USB dual-role controller driver programming reference](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt628026(v=vs.85))（USB 双角色控制器驱动程序编程参考）

## <a name="related-topics"></a>相关主题
[USB 双角色驱动程序堆栈体系结构](usb-dual-role-driver-stack-architecture.md)  



