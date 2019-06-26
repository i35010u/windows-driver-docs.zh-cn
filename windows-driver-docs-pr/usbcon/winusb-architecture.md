---
Description: WinUSB 包含两个主要组件-Winusb.sys、 内核模式驱动程序和 Winusb.dll-用户模式 DLL。
title: WinUSB 体系结构和模块
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcf343743493aa12fe9d8c843b2ed322b9e8091c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385692"
---
# <a name="winusb-architecture-and-modules"></a>WinUSB 体系结构和模块


[WinUSB](winusb.md)两个主要组件组成：

-   Winusb.sys 是可以作为筛选器或函数的驱动程序，上述的 USB 设备的内核模式设备堆栈中的协议驱动程序安装一个内核模式驱动程序。
-   Winusb.dll 是公开的用户模式 DLL [WinUSB 函数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)。 应用程序可以使用这些函数以将其作为设备的功能驱动程序安装时与 Winusb.sys 进行通信。

对于不需要自定义功能驱动程序的设备，Winusb.sys 可以安装在设备的内核模式堆栈为功能驱动程序。 用户模式进程然后可以通过使用一系列设备 I/O 控制请求或调用与 Winusb.sys 通信[WinUSB 函数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)。

下图显示了包含多个实例的 Winusb.sys 的 USB 驱动程序堆栈。

![winusb 驱动程序和设备对象堆栈](images/winusb-architecture.png)

上图显示了示例 WinUSB 配置实现三个设备接口类，其中每个单个注册的设备接口：

-   第 1 个 Winusb.sys 实例注册设备接口一个，支持用户模式驱动程序 (Usboem.dll)。
-   第 2 个 Winusb.sys 实例注册为使用一种系统服务 (SVCHOST) 与 Winusb.dll 通信的扫描仪 (Usbscan.exe) 支持用户模式驱动程序的设备接口 B。
-   3 个 Winusb.sys 注册设备接口 C，它支持固件更新实用程序 (Usbfw.exe)。

没有 Winusb.sys 的一个加载的实例。 PDO 可以表示非复合设备 （例如，实例 1 在关系图中），也可以表示的接口或复合设备 （例如，实例 2 和 3） 上的接口集合。 对于 USB 无线移动通信设备类 (WMCDC) 设备，PDO 甚至可以表示多个接口集合。 (有关 PDOs WMCDC 设备的详细信息，请参阅[支持无线移动通信设备类](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)。)

任何用户模式应用程序可与 USB 堆栈通信通过加载 WinUSB 动态链接库 (Winusb.dll) 并调用此模块公开的 WinUSB 函数。

## <a name="related-topics"></a>相关主题
[WinUSB (winusb.sys) 安装](winusb-installation.md)  
[如何通过使用 WinUSB 函数访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)  
[针对管道策略修改 WinUSB 函数](winusb-functions-for-pipe-policy-modification.md)  
[WinUSB 电源管理](winusb-power-management.md)  
[WinUSB 函数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)  
[WinUSB](winusb.md)  



