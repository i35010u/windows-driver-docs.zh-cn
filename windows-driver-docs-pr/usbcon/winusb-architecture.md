---
description: WinUSB 包含两个主要组件-Winusb.sys、内核模式驱动程序和 Winusb.dll 用户模式 DLL。
title: WinUSB 体系结构和模块
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3194aae9d7639f1cb822885a95275339b69e349e
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969038"
---
# <a name="winusb-architecture-and-modules"></a>WinUSB 体系结构和模块


[WinUSB](winusb.md) 包含两个主要组件：

-   Winusb.sys 是一种内核模式驱动程序，可作为筛选器或功能驱动程序安装在 USB 设备内核模式设备堆栈中的协议驱动程序之上。
-   Winusb.dll 是公开 [WinUSB 函数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)的用户模式 DLL。 当应用程序安装为设备的功能驱动程序时，应用程序可以使用这些功能与 Winusb.sys 进行通信。

对于不需要自定义函数驱动程序的设备，Winusb.sys 可以作为函数驱动程序安装在设备的内核模式堆栈中。 然后，用户模式进程可以通过使用一组设备 i/o 控制请求或通过调用 [WinUSB 函数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)与 Winusb.sys 进行通信。

下图显示了包含多个 Winusb.sys 实例的 USB 驱动程序堆栈。

![winusb 驱动程序和设备对象堆栈](images/winusb-architecture.png)

上图显示了实现三个设备接口类的示例 WinUSB 配置，其中每个类都有一个已注册的设备接口：

-   Winusb.sys 的实例1注册了设备接口 A，它支持用户模式驱动程序 ( # A1) 。
-   Winusb.sys 的实例2注册了设备接口 B，该接口支持通过使用系统服务 (SVCHOST) 与 Winusb.dll 通信的扫描仪 ( # A1) 的用户模式驱动程序。
-   Winusb.sys 的实例3注册了支持固件更新实用程序 ( # A1) 的设备接口 C。

只有一个 Winusb.sys 加载的实例。 PDO 可以表示非复合设备 (例如，关系图) 中的实例1，也可以表示复合设备上的接口或接口集合 (例如，实例2和 3) 。 对于 USB 无线移动通信设备类 (WMCDC) 设备，PDO 甚至可以表示多个接口集合。  (有关 WMCDC 设备的 PDOs 的详细信息，请参阅 [支持无线移动通信设备类](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)。 ) 

任何用户模式应用程序都可以通过加载 WinUSB 动态链接库 ( # A0) 并调用此模块公开的 WinUSB 函数，与 USB 堆栈进行通信。

## <a name="related-topics"></a>相关主题
[WinUSB ( # A0) 安装](winusb-installation.md)  
[如何通过 WinUSB 函数访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)  
[用于管道策略修改的 WinUSB 函数](winusb-functions-for-pipe-policy-modification.md)  
[WinUSB 电源管理](winusb-power-management.md)  
[WinUSB 函数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)  
[WinUSB](winusb.md)  



