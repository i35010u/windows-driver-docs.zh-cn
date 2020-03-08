---
title: 文件系统在系统启动期间会发生什么情况
description: 文件系统在系统启动期间会发生什么情况
ms.assetid: f6ed556a-2353-4a0d-8db1-1fb5eac3c1ef
keywords:
- 旧筛选器驱动程序 WDK 文件系统、启动过程
- 旧文件系统筛选器驱动程序 WDK，启动过程
- 旧式文件系统驱动程序 WDK，启动过程
- 文件系统识别器 WDK
- FsRec WDK
- 旧筛选器驱动程序 WDK 文件系统，驱动程序加载
- 旧文件系统筛选器驱动程序 WDK，驱动程序加载
- 驱动程序加载 WDK 文件系统
- 正在加载驱动程序 WDK 文件系统
- 加载顺序组 WDK 文件系统
- 重新初始化例程文件系统
- 启动驱动程序 WDK 文件系统
- 启动驱动程序 WDK 文件系统
- 全局文件系统队列 WDK 文件系统
- 文件系统队列 WDK
- 队列 WDK 文件系统
- FsRec
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 740187d7bdfa5770d7bde74d6804beb9c7cc643d
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910444"
---
# <a name="what-happens-to-file-systems-during-system-boot"></a>文件系统在系统启动期间会发生什么情况

> [!NOTE]
> 为了获得最佳的可靠性和性能，请使用带有筛选器管理器支持的[文件系统微筛选器驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-concepts)，而不是使用旧的文件系统 若要将旧驱动程序移植到微筛选器驱动程序，请参阅[迁移旧筛选器驱动程序的准则](guidelines-for-porting-legacy-filter-drivers.md)。

文件系统在系统启动过程中进行初始化;具体而言，在 i/o 系统初始化过程中。 I/o 管理器会创建全局文件系统队列，并初始化操作系统（OS）加载程序和 PnP 管理器加载的文件系统和旧筛选器驱动程序。

## <a name="system-boot-process"></a>系统启动过程

下面是对文件系统和旧式筛选器驱动程序开发人员感兴趣的系统引导过程的选定部分的摘要。

1. 在系统启动过程中，操作系统加载程序会在加载程序将控制转移到内核之前，加载启动文件系统、原始文件系统以及 SERVICE_BOOT_START 类型的所有驱动程序。 当内核获得控制时，这些驱动程序将在内存中。

   驱动程序按照它们所分配到的加载顺序组的顺序进行加载。 在文件系统筛选器中，分配给一个新的文件系统筛选器驱动程序加载顺序组的筛选器将在所有其他筛选器驱动程序之前加载。 [文件系统筛选器驱动程序的加载顺序组](load-order-groups-for-file-system-filter-drivers.md)中详细介绍了这些加载顺序组。

   然后，将加载 "筛选器" 加载顺序组中的所有驱动程序。 请注意，"筛选器" 组包括存储筛选器驱动程序和文件系统筛选器驱动程序，并且它包括第三方和内置筛选器驱动程序。

2. I/o 管理器会创建一个具有四个段的全局文件系统队列，每个段分别用于 CD-ROM、磁盘、磁带设备和网络文件系统。 稍后，当注册每个文件系统时，其控制设备对象将添加到此队列的适当段。 然而，此时尚未注册任何文件系统，因此队列为空。

3. PnP 管理器调用原始文件系统和所有 SERVICE_BOOT_START 驱动程序的[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程。

   如果 SERVICE_BOOT_START 驱动程序依赖于其他驱动程序，则也会加载并启动这些驱动程序。

   PnP 管理器通过调用启动设备驱动程序的[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程来启动启动设备。 如果启动设备具有子设备，则会枚举这些设备。 如果子设备的驱动程序是启动启动驱动程序，也会配置并启动子设备。 如果设备的驱动程序并非所有启动启动驱动程序，则 PnP 管理器会为设备创建 devnode，但不会启动设备。

   此时会加载所有启动驱动程序并启动启动设备。

4. PnP 管理器遍历[pnp 设备树](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)，查找并加载与每个 devnode 相关联但尚未运行的驱动程序。

   每个 PnP 设备启动时，PnP 管理器会枚举设备的子节点（如果有）。 PnP 管理器配置子设备，加载其设备驱动程序，并启动设备。

   PnP 管理器加载每个设备的驱动程序，*而不考虑*驱动程序的 " **StartType**"、" **LoadOrderGroup**" 或 "**依赖项**" 值。

   在此步骤中，PnP 管理器仅配置并启动可 PnP 枚举的设备。 如果设备不是 PnP 可枚举设备，则 PnP 管理器会忽略设备，并且不会枚举其子代，即使子设备是 PnP 可枚举的。

5. PnP 管理器加载并初始化尚未加载 SERVICE_SYSTEM_START 类型的驱动程序。

   此时将加载文件系统识别器（FsRec）。 请注意，尽管它位于 "启动文件系统" 加载顺序组，但 FsRec 不是启动文件系统。 实际启动文件系统（即装载启动卷的文件系统）是在启动过程开始时加载的。

   稍后在 SERVICE_SYSTEM_START 阶段，将加载 "文件系统" 加载顺序组中的文件系统。 这包括命名管道文件系统（NPFS）和 Mailslot 文件系统（MSFS）。 它不包括基于媒体的文件系统，例如 NTFS、FAT、CDFS 或 UDF。

   "网络" 加载顺序组中的网络文件系统也会在此阶段加载。

6. 在启动时加载的所有驱动程序都已初始化后，i/o 管理器将调用具有这些驱动程序的任何驱动程序的重新初始化例程。 重新*初始化例程*是由启动驱动程序注册的回调例程，该启动驱动程序需要在启动过程中指定额外的处理时间。 重新初始化例程是通过调用[**IoRegisterBootDriverReinitialization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioregisterbootdriverreinitialization)或[**IoRegisterDriverReinitialization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioregisterdriverreinitialization)注册的。

7. 服务控制管理器加载尚未加载 SERVICE_AUTO_START 类型的驱动程序。

## <a name="file-system-recognizer"></a>文件系统识别器

系统启动后，将加载并启动附加到系统的所有卷的存储设备驱动程序。 但是，并非所有内置文件系统都已加载，且并非所有文件系统卷都已装入。 文件系统识别器（FsRec）根据需要执行这些任务来处理[**IRP_MJ_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)请求。

FsRec 在系统启动的 SERVICE_SYSTEM_START 阶段中加载。 请注意，尽管它位于 "启动文件系统" 加载顺序组，但 FsRec 不是启动文件系统。 实际启动文件系统（即装载启动卷的文件系统）是在启动过程开始时加载的。
