---
title: 更换器类驱动程序版本中的差异
description: 更换器类驱动程序版本中的差异
keywords:
- 更换器驱动程序 WDK 存储，类驱动程序
- 存储更换器驱动程序 WDK、类驱动程序
- 类驱动程序 WDK 存储，更换器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55e433c175a0df5ef388bdc8a3b040c056fd0b87
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804677"
---
# <a name="differences-in-changer-class-driver-versions"></a>更换器类驱动程序版本中的差异


## <span id="ddk_differences_in_changer_class_driver_versions_kg"></span><span id="DDK_DIFFERENCES_IN_CHANGER_CLASS_DRIVER_VERSIONS_KG"></span>


在 Windows XP 和 Windows 2000 中，转换器类/miniclass 驱动程序对的实现有三个主要区别：

1.  Miniclass 驱动程序中 [**DriverEntry 的转换器 Miniclass 驱动程序**](./driverentry-of-changer-miniclass-drivers.md) 例程的不同用法。

    在 Windows 2000 中，变换器类驱动程序的 **DriverEntry** 例程执行各种驱动程序初始化任务，包括初始化 i/o 请求的入口点。 在 Windows XP 和更高版本的操作系统中，将在 miniclass 驱动程序的 **DriverEntry** 例程中进行初始化。 请参阅 [所需的转换器 Miniclass 例程](required-changer-miniclass-routines.md) ，详细了解 Miniclass Driver 的 **DriverEntry** 例程需要执行的任务。

2.  访问 *classpnp.sys* 库例程的不同方式。

    磁盘、磁带、cd-rom 和转换器设备的类驱动程序使用 *classpnp.sys* 库，这是一个系统提供的 DLL，其中包含一系列特定于操作系统、与设备无关的例程。

    大多数系统提供的存储类驱动程序提供一组类似于在 *classpnp.sys* 库中找到的例程的密钥例程。 这样做是为了使其 miniclass 驱动程序可以调用类驱动程序例程，而不是直接调用 *classpnp.sys。* 这会阻止 miniclass 驱动程序对 *classpnp.sys* DDI 的更改。

    Windows 2000 变换器 miniclass 驱动程序是此规则的例外情况，因为在 Windows 2000 中，变换器类驱动程序不会为 miniclass 驱动程序提供可间接调用 *classpnp.sys* 例程的工具。 因此，在 Windows 2000 中，变换器 miniclass 驱动程序必须直接调用 *classpnp.sys* 例程，或逐行调用等效的例程。 直接调用 *classpnp.sys* 例程的 Miniclass 驱动程序必须以静态方式链接到 *classpnp.sys* 库，大军驱动程序的大小。 如果驱动程序动态链接到 *classpnp.sys*，则在后续版本中对此库所做的更改可能会导致驱动程序无法正常工作。

    在 Windows XP 及更高版本的操作系统中，先前通过直接调用 *classpnp.sys* 库提供的几个最重要的服务由变换器类驱动程序提供。 因此，在 Windows XP 和更高版本的操作系统中，转换器 miniclass 驱动程序通常不需要直接调用 *classpnp.sys* 库例程。

3.  Windows XP 变换器类驱动程序提供了 Windows 2000 中不可用的例程。 下面讨论了这种差异。

在 Windows 2000 中，变换器类驱动程序为要调用的 miniclass 驱动程序提供以下例程：

-   [**ChangerClassAllocatePool**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changerclassallocatepool) --分配池内存。

-   [**ChangerClassFreePool**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changerclassfreepool) --释放池内存。

-   [**ChangerClassDebugPrint**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changerclassdebugprint) --打印调试信息。

在 Windows XP 及更高版本的操作系统中，变换器类驱动程序除了提供前面列出的例程外，还提供两个附加的例程。

-   [**ChangerClassInitialize**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changerclassinitialize) --转换器 miniclass 驱动程序从其 **DriverEntry** 例程中调用 **ChangerClassInitialize** 以初始化驱动程序。 **ChangerClassInitialize** 执行以前由 Windows 2000 变换器类驱动程序的 **DriverEntry** 例程执行的许多任务。

-   [**ChangerClassSendSrbSynchronous**](/windows-hardware/drivers/ddi/mcd/nf-mcd-changerclasssendsrbsynchronous) --初始化并将 SRB 同步发送到指定的目标设备。

 

