---
title: 文件系统筛选器驱动程序使用的设备对象的类型
description: 文件系统筛选器驱动程序使用的设备对象的类型
keywords:
- 目标设备对象 WDK 文件系统
- 筛选设备对象 WDK 文件系统
- 设备对象 WDK 文件系统
- 控制设备对象 WDK 文件系统
- CDOs WDK 文件系统
- FDOs WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 108c4295ad1fa5d0076a5dfbbb263ebaf31404bb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841133"
---
# <a name="types-of-device-objects-used-by-file-system-filter-drivers"></a>文件系统筛选器驱动程序使用的设备对象的类型


## <span id="ddk_types_of_file_system_filter_driver_device_objects_if"></span><span id="DDK_TYPES_OF_FILE_SYSTEM_FILTER_DRIVER_DEVICE_OBJECTS_IF"></span>


若要为 Irp 和快速 i/o 请求编写有效的调度例程，必须了解筛选器驱动程序可通过其接收这些请求的各种类型的目标设备对象。

与即插即用 (PnP) 设备（如磁盘驱动器）的驱动程序不同，文件系统筛选器驱动程序不会创建功能或物理设备对象。 而是创建控制设备对象并筛选设备对象。 *控制设备对象* (CDO) 表示系统和用户模式应用程序的筛选器驱动程序。 筛选 *器设备对象* (筛选器执行) 执行筛选特定文件系统或卷的实际工作。 文件系统筛选器驱动程序通常会创建一个 CDO 和一个或多个筛选器 DOs。

对于筛选器驱动程序收到的每种类型的 i/o 请求，目标设备对象可以是下列一项或多项：

-   筛选器驱动程序的 CDO 未连接到驱动程序堆栈

-   位于全局文件系统队列中文件系统 CDO 上方的筛选器设备对象

-   链接到已装载的文件系统卷设备对象 (VDO 的筛选器设备对象) 

筛选器驱动程序只能为 Irp 注册一组调度例程，为快速 i/o 请求注册一个。 因此，每种类型的请求必须由单个例程处理。 此例程必须确定上面列出的哪些目标设备对象收到请求，以便它能够相应地处理请求。

本节包括：

[筛选器驱动程序的控制设备对象](the-filter-driver-s-control-device-object.md)

[筛选附加到文件系统的设备对象](filter-device-object-attached-to-a-file-system.md)

[筛选连接到卷的设备对象](filter-device-object-attached-to-a-volume.md)

 

 




