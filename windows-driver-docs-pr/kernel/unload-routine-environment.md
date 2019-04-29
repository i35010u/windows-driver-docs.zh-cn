---
title: Unload 例程环境
description: Unload 例程环境
ms.assetid: 4acf66f1-7b97-494e-9f84-14292e971542
keywords:
- 卸载例程 WDK 内核环境
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbc932522fa7684bd8546b4533480463ae7a921e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355287"
---
# <a name="unload-routine-environment"></a>Unload 例程环境





该驱动程序将被替换或时，操作系统卸载驱动程序的所有设备驱动程序服务已删除。 PnP 管理器调用即插即用驱动程序的[ *Unload* ](https://msdn.microsoft.com/library/windows/hardware/ff564886)例程没有更多的设备驱动程序是否对象后它处理[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738)请求。

在开始卸载序列时，I/O 管理器或 PnP 管理器将标记的驱动程序对象和其设备对象为"卸载挂起"。 驱动程序已被标记为"卸载挂起"后，没有其他驱动程序可以将附加到该驱动程序，也可以对驱动程序的设备对象进行的任何其他引用。 该驱动程序可以完成未完成的 Irp，但系统不会向驱动程序发送任何新 Irp。

I/O 管理器调用的驱动程序*Unload*例程满足所有以下时：

-   没有引用保持到任何驱动程序已创建的设备对象。 换而言之，没有与基础设备关联的文件可以打开，也可以是任何 Irp 的驱动程序的设备对象中的任何未完成。

-   没有其他驱动程序保持附加到此驱动程序。

-   该驱动程序已调用[ **IoUnregisterPlugPlayNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff550398)撤消注册为其它以前注册的所有即插即用通知。

请注意， *Unload*如果驱动程序不调用例程[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程将返回失败状态。 在这种情况下，I/O 管理器只是释放该驱动程序所占用的内存空间。

PnP 管理器和 I/O 管理器都不调用*Unload*例程在系统关闭时。 必须执行关闭处理的驱动程序应注册[ *DispatchShutdown* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。

 

 




