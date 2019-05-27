---
Description: 此部分提供的 USB 外围设备制造商的链接。
title: 为 Windows 构建 USB 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb488088da80399a6d7d1e3d82fa1a978a70f5c2
ms.sourcegitcommit: bb482ef6935e171674c6a99bb499668c0f62ca24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66051643"
---
# <a name="building-usb-devices-for-windows"></a>为 Windows 构建 USB 设备

## <a name="summary"></a>总结

* USB 设备构建者的资源

此部分提供的 USB 外围设备制造商的链接。

## <a name="usb-device-enumeration-process"></a>USB 设备枚举进程

[USB 堆栈如何枚举设备？](https://go.microsoft.com/fwlink/p/?linkid=617517)  
由 Microsoft USB 驱动程序堆栈-从堆栈时检测设备存在并且指示 PnP 管理器已到达新的设备在枚举过程详细的说明。

[USB 2.1，2.0，1.1 Windows 8 中的设备枚举更改](https://go.microsoft.com/fwlink/p/?linkid=617518)  
在 Windows 8 中，我们进行了修改中如何堆栈枚举 2.1、 2.0 和 1.1 的 USB 设备的 USB 驱动程序堆栈中。 这些修改支持 USB 的新功能和改进设备枚举性能。 读取发布的内容以使意识到这些细微的更改并启用设备/固件构建者能够轻松地确定枚举失败的根本原因。

## <a name="microsoft-os-descriptors"></a>Microsoft OS 描述符

USB 设备在设备和其接口和终结点的固件中存储标准描述符。 此外，设备可以存储类和特定于供应商的描述符。 但是，这些描述符可以包含的类型是信息的有限的。 Ihv 通常必须使用 Windows 更新或媒体 Cd 如要为其用户提供的各种特定于设备的信息，如图片、 图标和自定义驱动程序。

IHV 可以使用 Microsoft OS 描述符来而不是单独提供的固件中存储的信息。 窗口通过阅读 Microsoft 操作系统描述符，检索该信息并使用它来安装和配置设备，而无需任何用户交互。 请参阅[USB 设备的 Microsoft 操作系统描述符](microsoft-defined-usb-descriptors.md)。

[1.0 的 Microsoft 操作系统描述符规范](https://go.microsoft.com/fwlink/p/?linkid=617519)  
本文档介绍 Microsoft 操作系统描述符。 它包括 OS 字符串描述符，扩展属性操作系统功能描述符和 OS 功能描述符格式规范。

[2.0 的 Microsoft 操作系统描述符规范](https://go.microsoft.com/fwlink/p/?linkid=306681)  
本文档定义，并描述了版本 2.0 的 Microsoft 操作系统描述符的实现。 Microsoft OS 2.0 描述符旨在解决的限制和可靠性问题的 1.0 版的操作系统描述符，并启用新的 USB 设备的特定于 Windows 的功能。

[加载 Winusb.sys 为功能驱动程序通过使用 Microsoft OS 描述符](automatic-installation-of-winusb.md)  
IHV 可以定义某些 Microsoft 操作系统 (OS) 功能描述符该报表的兼容 ID 为"WINUSB"。 这些描述符允许 Windows 加载 Winusb.sys 作为设备的功能驱动程序不使用自定义的 INF 文件。 有关如何定义兼容 ID 的示例，请参阅扩展兼容 ID 操作系统功能描述符规范的示例部分。 下载中包含规范[Microsoft 操作系统 1.0 描述符规范](https://go.microsoft.com/fwlink/p/?linkid=617519)。

## <a name="setting-a-container-id"></a>设置容器 ID

[USB 设备的容器 Id](https://msdn.microsoft.com/library/windows/hardware/ff540084)  
介绍如何生成通用串行总线 (USB) 设备的容器 Id。

[在 Windows 中的 USB ContainerIDs](usb-containerids-in-windows.md)  
面向设备制造商，以便它们可以正确检测由 Windows 编程其多功能的 USB 设备的指导原则。

[如何为 USB 设备生成的容器 ID](https://go.microsoft.com/fwlink/p/?linkid=617520)  
博客文章介绍了如何在设备必须报告容器 ID 如此一来，Windows 枚举并显示在设备**设备和打印机**正确。 对于支持多个函数 （复合设备） 或组件 （复合设备） 的设备，设备必须报告为每个部分相同的 ID。 设备必须报告 Microsoft OS ContainerID 描述符中的 ID。

## <a name="implementing-power-management"></a>实施电源管理

[USB 3.0 硬件中的链接电源管理](link-power-management-in-usb-3-0-hardware.md)  
本文档提供用于与选择性挂起结合使用链接电源管理 (LPM) 实现 USB 设备的电源管理硬件供应商和 Oem 的指导原则。 它介绍了从 U1 到 U2 的硬件转换并提供有关 USB 控制器、 中心和设备中的 LPM 实现中的常见缺陷的信息。

[揭秘选择性挂起](link-power-management-in-usb-3-0-hardware.md)  
此博客文章介绍了如何 USB 驱动程序堆栈处理函数和选择性挂起在 USB 3.0 设备。

## <a name="debugging-and-diagnostic-tools"></a>调试和诊断工具

[USB Windows 事件跟踪](usb-event-tracing-for-windows.md)  
Windows 事件跟踪 (ETW) 是一种高速通用的跟踪工具，由操作系统提供。 它包括有关如何安装工具、 创建跟踪文件和分析 USB 跟踪文件中的事件的信息。

[WPP 软件跟踪](https://msdn.microsoft.com/library/windows/hardware/ff556204)  
如何使用默认操作的 Windows 软件跟踪预处理器 (WPP) 来跟踪软件组件 （跟踪提供程序） 的操作。

[USB 3.0 扩展](https://msdn.microsoft.com/library/windows/hardware/hh869258)(usb3kd.dll)  
这些命令将显示由三个 USB 3.0 堆栈中的驱动程序维护的数据结构中的信息： USB 3.0 集线器驱动程序、 USB 主控制器扩展驱动程序和 USB 3.0 主机控制器驱动程序。

[USB 2.0 扩展](https://msdn.microsoft.com/library/windows/hardware/dn367056)(usb2kd.dll)  
这些命令将显示由 USB 2.0 堆栈中的驱动程序维护的数据结构中的信息： USB 2.0 中心驱动程序和 USB 2.0 主机控制器驱动程序。

## <a name="related-topics"></a>相关主题

[通用串行总线 (USB)](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
