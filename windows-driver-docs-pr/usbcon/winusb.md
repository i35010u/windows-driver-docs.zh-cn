---
Description: 本部分介绍通用 WinUSB 驱动程序 (Winusb.sys) 和其由 Microsoft 提供的所有 USB 设备的用户模式组件 (Winusb.dll)。
title: WinUSB (Winusb.sys)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 432ffe606066b576fcdb730b847b55a578b9959b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385345"
---
# <a name="winusb-winusbsys"></a>WinUSB (Winusb.sys)


本部分介绍通用 WinUSB 驱动程序 (Winusb.sys) 和其由 Microsoft 提供的所有 USB 设备的用户模式组件 (Winusb.dll)。

在 Windows 的以前版本 Windows XP Service Pack 2 (SP2)，所有 USB 设备驱动程序都需要在内核模式下操作。 如果创建了操作系统没有本机类驱动程序为其一个 USB 设备，你必须编写您的设备的内核模式设备驱动程序。

Windows USB (WinUSB) 是为带有 SP2 的 Windows XP 开发的 Windows 驱动程序框架 (WDF) 与并发有关 USB 设备的通用驱动程序。 WinUSB 体系结构包括内核模式驱动程序 (Winusb.sys) 和用户模式动态链接库 (Winusb.dll) 公开[WinUSB 函数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)。 通过使用这些函数，可以管理用户模式软件的 USB 设备。

Winusb.sys 也是链接的 UMDF 功能驱动程序和关联的设备之间的重要组成部分。 Winusb.sys 作为上限的筛选器驱动程序安装在设备的内核模式堆栈中。 应用程序与设备的 UMDF 功能驱动程序发出的读取、 写入或设备的 I/O 控制请求进行通信。 该驱动程序框架，它将请求传递给 Winusb.sys 与进行交互。 Winusb.sys 然后处理请求，并将其传递给协议驱动程序并最终移到设备。 按反向路径返回任何响应。 Winusb.sys 也可作为设备堆栈插和 power 所有者。

**请注意**  WinUSB 函数需要 Windows XP 或更高版本。 可以在 C 中使用这些函数 /C++应用程序与您的 USB 设备进行通信。 Microsoft 不提供有关 WinUSB 托管的 API。

本部分介绍如何使用 WinUSB 与 USB 设备进行通信。 在本部分中的主题提供有关选择正确的驱动程序为你的设备，安装 Winusb.sys 为 USB 设备的功能驱动程序，并包含代码示例，说明的详细的演练信息的指导原则如何应用程序和 USB 设备与彼此通信。

本部分包括以下主题：

-   [WinUSB 体系结构和模块](winusb-architecture.md)
-   [WinUSB (Winusb.sys) 安装](winusb-installation.md)
-   [WinUSB 设备](automatic-installation-of-winusb.md)
-   [如何通过使用 WinUSB 函数访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)
-   [针对管道策略修改 WinUSB 函数](winusb-functions-for-pipe-policy-modification.md)
-   [WinUSB 电源管理](winusb-power-management.md)

## <a name="windows-support-for-winusb"></a>Windows 支持 WinUSB


下表汇总了 WinUSB 支持不同版本的 Windows 中。

| Windows 版本      | WinUSB 支持 |
|----------------------|----------------|
| Windows 10 及更高版本 | Yes²           |
| Windows 7            | Yes¹           |
| Windows Server 2008  | Yes²           |
| Windows Vista        | Yes²           |
| Windows Server 2003  | 否             |
| Windows XP           | Yes³           |
| Windows 2000         | 否             |

 

**请注意**   Yes¹:此版本的 Windows 支持 WinUSB 基于 x86 的、 基于 x64 和基于 Itanium 的系统上的所有 Sku。

Yes²:此版本的 Windows 支持 WinUSB 基于 x86 和基于 x64 的系统上的所有 Sku。

Yes³:所有客户端 Sku 的 Windows XP SP2 service pack 支持 WinUSB。 WinUSB 不是本机转到 Windows XP;它必须与 WinUSB 共同安装程序安装。

不：在此版本的 Windows 不支持 WinUSB。

 

## <a name="usb-features-supported-by-winusb"></a>支持的 WinUSB USB 功能


下表显示了 WinUSB 支持不同版本的 Windows 中的高级 USB 功能。

| 功能                                | Windows 8.1 及更高版本 | Windows 7/Vista/XP |
|----------------------------------------|-----------------------|--------------------|
| 设备 I/O 控制请求            | 支持             | 支持          |
| 同步传输                  | 支持             | 不支持      |
| 大容量、 控制和中断传输 | 支持             | 支持          |
| 选择性挂起                      | 支持             | 支持          |
| 远程唤醒                            | 支持             | 支持          |

 

## <a name="related-topics"></a>相关主题
[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)  



