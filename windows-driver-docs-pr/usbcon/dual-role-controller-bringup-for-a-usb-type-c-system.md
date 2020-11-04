---
description: USB 角色切换驱动程序及其用于处理双重角色控制器的角色切换功能的客户端驱动程序。
title: 为 USB 类型 C Windows 系统启动双角色控制器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf79e76436b965789513065d80723f7e4cf5ec0e
ms.sourcegitcommit: ec7bebe3f94536455e62b372c2a28fe69d1717f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2020
ms.locfileid: "93349733"
---
# <a name="bring-up-the-dual-role-controller-for-a-usb-type-c-windows-system"></a>为 USB 类型 C Windows 系统启动双角色控制器

## <a name="summary"></a>总结

- OEM 为具有 USB 类型 C 连接器的双重角色控制器引入任务

## <a name="applies-to"></a>适用于

- Windows 10 移动版

## <a name="important-apis"></a>重要的 API

- [USB 双角色控制器驱动程序编程参考](/previous-versions/windows/hardware/drivers/mt628026(v=vs.85))

USB 角色切换驱动程序 (URS) 是一组 WDF 类扩展和处理双重角色控制器的角色切换功能的客户端驱动程序。 如果你的系统具有双重角色控制器，则你可以根据连接到系统的 USB 类型 C 连接器的合作伙伴端口的设备，来切换系统的角色。 这就允许有兴趣的方案，如有线停靠。

系统可设计为双角色 USB 控制器需要 Windows 将其配置为主机或函数模式。 这些设计使用 USB 角色切换堆栈。 如果系统不使用 Synopsys 或 ChipIdea 双重角色控制器，则需要为系统的双角色控制器写入 USB 角色切换客户端驱动程序。

>[!NOTE]
> 系统可设计为双重角色 USB 端口需要 Windows 将其配置为主机或函数模式。 这些设计使用 USB 角色切换堆栈。 如果系统未使用 Synopsys 双重角色控制器，则需要为系统的双角色控制器写入 USB 角色切换客户端驱动程序。

客户端驱动程序处理硬件事件并将其报告给类扩展。 对于角色切换硬件事件，URS 决定角色，并因此加载该角色的驱动程序。 如果控制器位于主机角色中，则会加载 [USB 主机端驱动程序](usb-3-0-driver-stack-architecture.md) ;对于函数角色，将加载 [设备端驱动程序](usb-device-side-drivers-in-windows.md) 。

在带有 USB 微 AB 连接器的系统上，双角色控制器的客户端驱动程序将使用分配给它的中断资源，根据连接器中的 ID pin 来做出此决定。 在使用 USB 类型 C 连接器的系统上，此决定由连接器的客户端驱动程序进行。 该驱动程序根据 "抄送" pin 确定角色，并将结果报告给 USB 连接器管理器 (UCM ") ，然后将结果发送到角色切换驱动程序。

![usb 角色切换驱动程序](images/urs.png)

## <a name="1-enable-the-urs-driver-in-system-acpi"></a>1. 在系统 ACPI 中启用 URS 驱动程序

若要使用 URS，必须进行 ACPI 修改。 将 [USB 设备端驱动程序](usb-device-side-drivers-in-windows.md) 加载的设备替换为必须加载 URS 的设备。 有关如何更改 ACPI 定义的详细信息，请参阅 [USB 双重角色驱动程序堆栈体系结构](usb-dual-role-driver-stack-architecture.md)中给定的示例。 请确保删除中断资源。 对于 USB 类型 C，这不是必需的。

## <a name="2-load-the-usb-role-switch-drivers-for-the-dual-role-controller-driver"></a>2. 为双重角色控制器驱动程序加载 USB 角色切换驱动程序

![usb 角色切换堆栈](images/urs.png)

- 如果系统使用 ChipIdea 和 Synopsys 控制器，请为 ChipIdea 和 Synopsys 控制器加载 Microsoft 提供的内置客户端驱动程序。

    若要加载驱动程序，必须创建驱动程序安装包。 INF 文件必须包含引用支持的控制器的内置 INF 的 **Include-需要** 指令。 内置 INF 已经包含其他控制器的硬件 Id。 如果你的双重角色控制器的硬件 ID 不是内置 INF 中的硬件 id 之一，则此步骤是必需的。 请与 SoC 供应商核实。

    有关详细信息，请参阅 " [驱动程序安装包](usb-dual-role-driver-stack-architecture.md)" 下的 "URS 驱动程序包"。

- 如果系统使用自定义控制器，则写入角色切换客户端驱动程序。 有关详细信息，请参阅：

    [USB 双角色控制器驱动程序编程参考](/previous-versions/windows/hardware/drivers/mt628026(v=vs.85))

## <a name="related-topics"></a>相关主题

[USB 双角色驱动程序堆栈体系结构](usb-dual-role-driver-stack-architecture.md)