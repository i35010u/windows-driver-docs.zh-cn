---
title: 文件系统筛选器驱动程序使用的设备对象的类型
description: 文件系统筛选器驱动程序使用的设备对象的类型
ms.assetid: e5662c95-71a0-49f8-a9d5-a03e2de1f426
keywords:
- 目标设备对象 WDK 文件系统
- 筛选设备对象 WDK 文件系统
- 设备对象 WDK 文件系统
- 控制设备对象 WDK 文件系统
- CDOs WDK 文件系统
- FDOs WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d03a99903327223ca4431a133fdcb1c2611de17b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563828"
---
# <a name="types-of-device-objects-used-by-file-system-filter-drivers"></a>文件系统筛选器驱动程序使用的设备对象的类型


## <span id="ddk_types_of_file_system_filter_driver_device_objects_if"></span><span id="DDK_TYPES_OF_FILE_SYSTEM_FILTER_DRIVER_DEVICE_OBJECTS_IF"></span>


若要编写有效的调度例程的 Irp 和快速 I/O 请求，务必了解不同类型的筛选器驱动程序可以通过其接收这些请求的目标设备对象。

插即用 (PnP) 设备，如磁盘驱动器的驱动程序与文件系统筛选器驱动程序不会创建功能或物理设备对象。 相反，它们创建设备对象的控件和筛选设备对象。 *控制设备对象*(CDO) 表示筛选器驱动程序与系统和用户模式应用程序。 *筛选设备对象*（筛选器执行操作） 执行实际工作的筛选特定文件系统或卷。 文件系统筛选器驱动程序通常将创建一个 CDO 和一个或多个筛选 DOs。

对于每个类型的筛选器驱动程序收到的 I/O 请求，目标设备对象可以是一个或多个以下：

-   筛选器驱动程序的 CDO，未附加到驱动程序堆栈

-   全局文件系统队列中的文件系统 CDO 上面链接筛选设备对象

-   上面已装载的文件系统卷设备对象 (VDO) 链接筛选设备对象

只有一组 Irp 的调度例程，另一个用于快速 I/O 请求，可以注册筛选器驱动程序。 因此，必须由单个例程处理每种类型的请求。 此例程必须确定哪些目标设备对象上面所列已收到请求，以便它可以适当地处理请求。

本部分包括：

[筛选器驱动程序的控制设备对象](the-filter-driver-s-control-device-object.md)

[筛选设备对象附加到文件系统](filter-device-object-attached-to-a-file-system.md)

[筛选设备对象附加到的卷](filter-device-object-attached-to-a-volume.md)

 

 




