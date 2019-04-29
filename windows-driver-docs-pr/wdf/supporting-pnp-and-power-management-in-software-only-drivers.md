---
title: 支持在仅限软件的驱动程序中进行 PnP 和电源管理
description: 支持在仅限软件的驱动程序中进行 PnP 和电源管理
ms.assetid: bcfca8b2-68d6-4875-8687-27351becd6f4
keywords:
- 即插即用 WDK KMDF，仅限软件的驱动程序
- 插 WDK KMDF，仅限软件的驱动程序
- 电源管理 WDK KMDF，仅限软件的驱动程序
- 仅限软件的驱动程序 WDK KMDF
- 筛选器驱动程序 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eeb96e085cbb0c3c087b24c8410465204174ea47
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363965"
---
# <a name="supporting-pnp-and-power-management-in-software-only-drivers"></a>支持在仅限软件的驱动程序中进行 PnP 和电源管理


*仅限软件的驱动程序*都不访问任何硬件的驱动程序。 仅限软件的某些驱动程序驻留在不访问硬件的驱动程序堆栈。 这些驱动程序不会访问硬件，因为它们通常不需要执行任何即插即用或电源管理操作。

仅限软件的其他驱动程序将筛选器驱动程序： 它们驻留在堆栈的驱动程序的执行访问硬件，但筛选器驱动程序不访问硬件。 当筛选器驱动程序收到指定即插即用的 I/O 请求或电源管理操作，该驱动程序通常只需将请求传递到下一步的驱动程序。 框架截获这些请求，并将其传递，以便基于框架的驱动程序永远不会看到请求。

如果您正在编写仅限软件的驱动程序，您的驱动程序[创建设备对象](creating-a-framework-device-object.md)但通常不需要提供用于处理即插即用或电源管理事件的回调函数的任何事件。 如果驱动程序使用[framework 队列对象](framework-queue-objects.md)，将需要设置**PowerManaged**的队列的成员[ **WDF\_IO\_队列\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552359)结构**WdfFalse**或**WdfUseDefault**。

几个仅限软件的驱动程序，还有[函数的驱动程序](supporting-pnp-and-power-management-in-function-drivers.md)。 换而言之，单个驱动程序可能会处理作为支持不会访问硬件的虚拟设备的纯软件驱动程序和功能驱动程序以支持硬件设备。

 

 





