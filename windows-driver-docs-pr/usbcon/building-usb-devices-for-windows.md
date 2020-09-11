---
description: 本部分提供了 USB 外围设备制造商的链接。
title: 为 Windows 构建 USB 设备的概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfaf7f37b397bc8e0e67eeffa39c77b3b2538dd5
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010302"
---
# <a name="overview-of-building-usb-devices-for-windows"></a>为 Windows 构建 USB 设备的概述

## <a name="summary"></a>摘要

* USB 设备生成器的资源

本部分提供了 USB 外围设备制造商的链接。

## <a name="usb-device-enumeration-process"></a>USB 设备枚举过程

[USB stack 如何枚举设备？](https://go.microsoft.com/fwlink/p/?linkid=617517)  
Microsoft USB 驱动程序堆栈所使用的枚举过程的详细说明-从堆栈检测到设备是否存在，向 PnP 管理器指示新设备已到达。

[USB 2.1，2.0，1.1 设备枚举在 Windows 8 中的更改](https://go.microsoft.com/fwlink/p/?linkid=617518)  
在 Windows 8 中，我们已在 azure 中的堆栈枚举 USB 2.1、2.0 和1.1 设备的方式中进行了修改。 这些修改支持新的 USB 功能并改善设备枚举性能。 阅读发布内容是使对这些细微变化的了解，使设备/固件构建者可以轻松地确定枚举失败的根本原因。

## <a name="microsoft-os-descriptors"></a>Microsoft OS 描述符

USB 设备将标准描述符存储在设备及其接口和终结点的固件中。 此外，设备还可以存储类和供应商特定的描述符。 但是，这些描述符可以包含的信息的类型会受到限制。 Ihv 通常必须使用 Windows 更新或媒体（如 Cd）为其用户提供各种设备特定的信息，如图片、图标和自定义驱动程序。

IHV 可以使用 Microsoft OS 描述符将信息存储在固件中，而不是单独提供。 窗口通过读取 Microsoft OS 描述符来检索该信息，并使用它来安装和配置设备，而无需任何用户交互。 请参阅 [MICROSOFT OS 描述符以获取 USB 设备](microsoft-defined-usb-descriptors.md)。

[Microsoft OS 1.0 描述符规范](https://go.microsoft.com/fwlink/p/?linkid=617519)  
本文档介绍 Microsoft 操作系统描述符。 它包含 OS 字符串描述符、扩展属性 OS 功能描述符和 OS 功能描述符格式的规范。

[Microsoft OS 2.0 描述符规范](./microsoft-os-2-0-descriptors-specification.md)  
本文档定义并说明 Microsoft OS 描述符版本2.0 的实现。 Microsoft 操作系统2.0 描述符的目标是解决操作系统描述符版本1.0 的限制和可靠性问题，并为 USB 设备启用特定于 Windows 的新功能。

[使用 Microsoft OS 描述符将 Winusb.sys 作为函数驱动程序加载](automatic-installation-of-winusb.md)  
IHV 可以定义某些 Microsoft 操作系统 (OS) 功能描述符，将兼容的 ID 报告为 "WINUSB"。 这些描述符允许 Windows 将 Winusb.sys 加载为设备的函数驱动程序，而无需使用自定义的 INF 文件。 有关如何定义兼容 ID 的示例，请参阅扩展兼容 ID OS 功能描述符规范的 "示例" 部分。 该规范包含在 [MICROSOFT 操作系统1.0 描述符规范](https://go.microsoft.com/fwlink/p/?linkid=617519)的下载中。

## <a name="setting-a-container-id"></a>设置容器 ID

[USB 设备的容器 ID](../install/how-usb-devices-are-assigned-container-ids.md)  
描述如何生成通用串行总线的容器 Id (USB) 设备。

[Windows 中的 USB ContainerID](usb-containerids-in-windows.md)  
适用于设备制造商对其多功能 USB 设备进行编程以使其能够由 Windows 正确检测的指导原则。

[如何生成 USB 设备的容器 ID](https://go.microsoft.com/fwlink/p/?linkid=617520)  
博客文章介绍了设备必须如何报告容器 ID，以便 Windows 在 **设备和打印机** 中正确地枚举并显示设备。 对于支持多个功能 (复合设备) 或组件 (复合设备) 的设备，设备必须报告每个部分的相同 ID。 设备必须在 Microsoft 操作系统 ContainerID 描述符中报告该 ID。

## <a name="implementing-power-management"></a>实现电源管理

[链接 USB 3.0 硬件中的电源管理](link-power-management-in-usb-3-0-hardware.md)  
本文档为硬件供应商和 Oem 提供准则，使其能够通过将链接电源管理 (LPM) 与选择性挂起结合使用来实现 USB 设备的电源管理。 它介绍了从 U1 到 U2 的硬件转换，并提供了有关 USB 控制器、集线器和设备中 LPM 实现的常见缺陷的信息。

[揭密选择性挂起](link-power-management-in-usb-3-0-hardware.md)  
此博客文章介绍 USB 驱动程序堆栈如何处理 USB 3.0 设备中的功能和选择性挂起。

## <a name="debugging-and-diagnostic-tools"></a>调试和诊断工具

[Windows 的 USB 事件跟踪](usb-event-tracing-for-windows.md)  
Windows (ETW) 的事件跟踪是由操作系统提供的通用、高速跟踪设备。 它包括有关如何安装这些工具、创建跟踪文件和分析 USB 跟踪文件中的事件的信息。

[WPP 软件跟踪](../devtest/wpp-software-tracing.md)  
如何使用 Windows 软件跟踪预处理器 (WPP) 的默认操作跟踪软件组件 (跟踪提供) 程序的操作。

[USB 3.0 扩展](../debugger/usb-3-extensions.md) ( # A0)   
这些命令显示 USB 3.0 堆栈中由三个驱动程序维护的数据结构中的信息： USB 3.0 集线器驱动程序、USB 主机控制器扩展驱动程序和 USB 3.0 主机控制器驱动程序。

[USB 2.0 扩展](../debugger/usb-2-0-extensions.md) ( # A0)   
这些命令显示由 USB 2.0 堆栈中的驱动程序维护的数据结构中的信息： USB 2.0 集线器驱动程序和 USB 2.0 主机控制器驱动程序。

## <a name="related-topics"></a>相关主题

[通用串行总线 (USB)](../index.yml)