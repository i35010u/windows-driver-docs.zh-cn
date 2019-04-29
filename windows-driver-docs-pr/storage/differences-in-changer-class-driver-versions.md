---
title: 更换器类驱动程序版本中的差异
description: 更换器类驱动程序版本中的差异
ms.assetid: 4ae4d1b0-cf2f-4c81-b8ae-3a91fd479a89
keywords:
- 更换器驱动程序 WDK 存储类驱动程序
- 存储更换器驱动程序 WDK、 类驱动程序
- 类驱动程序 WDK 存储，更换器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c68c604a9722e02287c75425b9d6d9a37974a5f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384842"
---
# <a name="differences-in-changer-class-driver-versions"></a>更换器类驱动程序版本中的差异


## <span id="ddk_differences_in_changer_class_driver_versions_kg"></span><span id="DDK_DIFFERENCES_IN_CHANGER_CLASS_DRIVER_VERSIONS_KG"></span>


有的转换器类/miniclass 驱动程序对在 Windows XP 和 Windows 2000 中实现的三个主要区别：

1.  不同的用[ **DriverEntry 的转换器 Miniclass 驱动程序**](https://msdn.microsoft.com/library/windows/hardware/ff552647)例程 miniclass 驱动程序中。

    在 Windows 2000，转换器类驱动程序**DriverEntry**例程执行不同的驱动程序初始化任务，包括输入/输出请求的入口点的初始化。 在 Windows XP 和更高版本操作系统中，初始化发生在**DriverEntry** miniclass 驱动程序的例程。 请参阅[需换带机 Miniclass 例程](required-changer-miniclass-routines.md)有关详细信息的任务的 miniclass 驱动程序**DriverEntry**执行所需的例程。

2.  其他方法来访问*classpnp.sys*库例程。

    使磁盘、 磁带、 CD-ROM 和换带机设备的类驱动程序使用的*classpnp.sys*库，系统提供的 DLL，其中包含特定于操作系统的、 独立于设备的例程的集合。

    大多数系统提供的存储类驱动程序提供的一组类似于例程中找到密钥例程*classpnp.sys*库。 这是，以便其 miniclass 驱动程序可以调用类驱动程序例程，而不是直接调用*classpnp.sys。* 这为屏蔽 miniclass 驱动程序从将变为*classpnp.sys* DDI。

    Windows 2000 换带机 miniclass 驱动程序是此规则的例外，因为在 Windows 2000 中的转换器类驱动程序不提供 miniclass 驱动程序使用一个工具，以便调用*classpnp.sys*例程间接。 因此，在 Windows 2000 中，换带机 miniclass 驱动程序必须调用*classpnp.sys*例程直接或调用行中的等效例程。 Miniclass 驱动程序调用*classpnp.sys*例程直接必须链接到*classpnp.sys*库以静态方式，swelling 驱动程序的大小。 如果驱动程序动态链接到*classpnp.sys*，对此库在后续版本中的更改可能会导致驱动程序无法正常工作。

    在 Windows XP 和更高版本操作系统中，多个最重要的服务以前提供的直接调用*classpnp.sys*库提供的转换器类驱动程序。 因此，在 Windows XP 和更高版本操作系统中，它是调用转换器 miniclass 的驱动程序通常不必要*classpnp.sys*直接库例程。

3.  在 Windows XP 转换器类驱动程序提供了例程在 Windows 2000 中不可用。 以下讨论介绍这种差异。

在 Windows 2000 中，在换带机类驱动程序提供 miniclass 驱动程序调用以下例程：

-   [**ChangerClassAllocatePool** ](https://msdn.microsoft.com/library/windows/hardware/ff551402) -分配池的内存。

-   [**ChangerClassFreePool** ](https://msdn.microsoft.com/library/windows/hardware/ff551411) -释放池内存。

-   [**ChangerClassDebugPrint** ](https://msdn.microsoft.com/library/windows/hardware/ff551406) -打印调试信息。

在 Windows XP 和更高版本操作系统中，提供了在换带机类驱动程序，除了例程之外的两个其他例程前面列出。

-   [**ChangerClassInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff551413) -换带机 miniclass 驱动程序调用**ChangerClassInitialize**中其**DriverEntry**例程，以初始化的驱动程序。 **ChangerClassInitialize**执行以前由 Windows 2000 转换器类驱动程序的执行的许多任务**DriverEntry**例程。

-   [**ChangerClassSendSrbSynchronous** ](https://msdn.microsoft.com/library/windows/hardware/ff551415) -初始化，并以同步方式将 SRB 发送到所指示的目标设备。

 

 




