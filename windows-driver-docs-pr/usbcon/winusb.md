---
description: 此部分介绍 Microsoft 为所有 USB 设备提供的通用 WinUSB 驱动程序 (Winusb.sys) 及其用户模式组件 (Winusb.dll)。
title: WinUSB (Winusb.sys)
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 44b82b6bad0ac92a84c89dd8b0851cb1d033e78b
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969222"
---
# <a name="winusb-winusbsys"></a>WinUSB (Winusb.sys)


此部分介绍 Microsoft 为所有 USB 设备提供的通用 WinUSB 驱动程序 (Winusb.sys) 及其用户模式组件 (Winusb.dll)。

在早于 Windows XP Service Pack 2 (SP2) 的 Windows 版本中，所有 USB 设备驱动程序都需要在内核模式下运行。 如果创建的 USB 设备的操作系统没有本机类驱动程序，则必须为设备编写内核模式设备驱动程序。

Windows USB (WinUSB) 是一种适用于 USB 设备的通用驱动程序，该驱动程序是与适用于 Windows XP SP2 的 Windows 驱动程序框架 (WDF) 同时开发的。 WinUSB 体系结构由内核模式驱动程序 (Winusb.sys) 和公开 [WinUSB 函数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)的用户模式的动态链接库 (Winusb.dll) 组成。 借助这些功能，你可以使用用户模式软件管理 USB 设备。

Winusb.sys 也是 UMDF 功能驱动程序与关联设备之间链接的关键部分。 Winusb.sys 作为上部筛选器驱动程序安装在设备的内核模式堆栈中。 应用程序与设备的 UMDF 函数驱动程序通信，以发出读取、写入或设备 I/O 控制请求。 驱动程序与框架交互，后者将请求传递到 Winusb.sys。 然后，Winusb.sys 处理请求并将其传递给协议驱动程序并最终传递到设备。 响应通过反向路径返回。 Winusb.sys 还充当设备堆栈的即插即用和电源所有者。

**注意**  WinUSB 函数需要 Windows XP 或更高版本。 可以在 C/C++应用程序中使用这些函数与 USB 设备通信。 Microsoft 不为 WinUSB 提供托管 API。

本部分介绍如何使用 WinUSB 与 USB 设备进行通信。 本部分中的主题提供有关为设备选择正确的驱动程序的指南、有关将 Winusb.sys 安装为 USB 设备的功能驱动程序的信息，以及包含显示应用程序和 USB 设备如何相互通信的代码示例的详细演练。

本部分包括以下主题：

-   [WinUSB 体系结构和模块](winusb-architecture.md)
-   [WinUSB (Winusb.sys) 安装](winusb-installation.md)
-   [WinUSB 设备](automatic-installation-of-winusb.md)
-   [如何通过 WinUSB Functions 访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)
-   [用于修改管道策略的 WinUSB 函数](winusb-functions-for-pipe-policy-modification.md)
-   [WinUSB 电源管理](winusb-power-management.md)

## <a name="windows-support-for-winusb"></a>Windows 对 WinUSB 的支持


下表汇总了不同版本的 Windows 中的 WinUSB 支持。

| Windows 版本      | WinUSB 支持 |
|----------------------|----------------|
| Windows 10 及更高版本 | 是²           |
| Windows 7            | 是¹           |
| Windows Server 2008  | 是²           |
| Windows Vista        | 是²           |
| Windows Server 2003  | 否             |
| Windows XP           | 是³           |
| Windows 2000         | 否             |

 

请注意     是¹：此 Windows 版本的所有 SKU 在基于 x86、基于 x64 和基于 Itanium 的系统上都支持 WinUSB。

是²：此 Windows 版本的所有 SKU 在基于 x86 和基于 x64 的系统上都支持 WinUSB。

是³：Windows XP SP2 Service Pack 的所有客户端 SKU 都支持 WinUSB。 WinUSB 不是 Windows XP 本机上的，它必须与 WinUSB 共同安装程序一起安装。

否：此 Windows 版本不支持 WinUSB。

 

## <a name="usb-features-supported-by-winusb"></a>WinUSB 支持的 USB 功能


下表显示了不同 Windows 版本中 WinUSB 支持的高级 USB 功能。

| 功能                                | Windows 8.1 和更高版本 | Windows 7/Vista/XP |
|----------------------------------------|-----------------------|--------------------|
| 设备 I/O 控制请求            | 支持             | 支持          |
| 常时等量传输                  | 支持             | 不受支持      |
| 大容量、控制和中断传输 | 支持             | 支持          |
| 选择性挂起                      | 支持             | 支持          |
| 远程唤醒                            | 支持             | 支持          |

 

## <a name="related-topics"></a>相关主题
[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)  



