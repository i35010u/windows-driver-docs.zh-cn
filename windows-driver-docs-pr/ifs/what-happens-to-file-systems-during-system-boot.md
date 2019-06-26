---
title: 文件系统在系统启动期间会发生什么情况
description: 文件系统在系统启动期间会发生什么情况
ms.assetid: f6ed556a-2353-4a0d-8db1-1fb5eac3c1ef
keywords:
- 筛选器驱动程序 WDK 文件系统、 引导过程
- 文件系统筛选器驱动程序 WDK，启动过程
- 文件系统驱动程序 WDK，启动过程
- 文件系统识别器 WDK
- FsRec WDK
- 筛选器驱动程序 WDK 文件系统，加载的驱动程序
- 文件系统筛选器驱动程序 WDK，加载的驱动程序
- 正在加载 WDK 文件系统驱动程序
- 加载驱动程序 WDK 文件系统
- 加载顺序组 WDK 文件系统
- 要重新初始化例程 WDK 文件系统
- 启动驱动程序 WDK 文件系统
- 引导启动驱动程序 WDK 文件系统
- 全局文件系统队列 WDK 文件系统
- 文件系统队列 WDK
- 队列 WDK 文件系统
- FsRec
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbf1c7cda65b48926cc824980c8a694a5b1f3f7c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380249"
---
# <a name="what-happens-to-file-systems-during-system-boot"></a>文件系统在系统启动期间会发生什么情况


## <span id="ddk_what_happens_to_file_systems_during_system_boot_if"></span><span id="DDK_WHAT_HAPPENS_TO_FILE_SYSTEMS_DURING_SYSTEM_BOOT_IF"></span>


在系统启动过程中; 初始化文件系统具体而言，在 I/O 系统的初始化。 I/O 管理器创建全局文件系统队列并初始化由操作系统 (OS) 加载程序和 PnP 管理器已加载的文件系统和筛选器驱动程序。

下面是在系统启动过程感兴趣的文件系统和筛选器驱动程序开发人员的选定部分的摘要。

1.  在系统启动期间 OS 加载程序加载引导文件系统、 原始文件系统和服务类型的所有驱动程序\_启动\_开始之前，加载程序将控制转移到内核。 当内核获取控件时，这些驱动程序是在内存中。

    驱动程序已加载的加载顺序组分配到顺序。 在文件系统筛选器，这些分配给一个新的文件系统筛选器驱动程序加载组的所有其他筛选器驱动程序之前加载的顺序。 中详细介绍了这些加载顺序组[文件系统筛选器驱动程序的加载顺序组](load-order-groups-for-file-system-filter-drivers.md)。

    然后在"筛选"加载顺序组的所有驱动程序已加载。 请注意，"筛选"组包括存储筛选器驱动程序，以及文件系统筛选器驱动程序，它包括第三方，以及内置筛选器驱动程序。

2.  I/O 管理器创建具有四个线段的全局文件系统的队列： 两个分别用于 CD-ROM、 磁盘、 磁带设备和网络文件系统。 更高版本，注册每个文件系统时，其控制的设备对象添加到此队列的适当段。 此时，但是，没有文件系统尚未已注册，因此队列为空。

3.  PnP 管理器调用[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程 RAW 文件系统和所有服务\_启动\_启动的驱动程序。

    如果服务\_启动\_启动驱动程序是依赖于其他驱动程序，这些驱动程序将加载并同时启动。

    PnP 管理器通过调用启动的启动设备[ **AddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程的启动设备驱动程序。 如果启动设备具有子设备，将枚举这些设备。 子设备还配置并启动其驱动程序是否引导启动驱动程序。 如果设备的驱动程序不是所有引导启动驱动程序，即插即用管理器创建设备 devnode，但不会启动设备。

    此时，所有启动驱动程序都加载并启动设备已启动。

4.  PnP 管理器遍历即插即用设备树中，查找并加载与每个 devnode 相关联的驱动程序但尚未运行。

    (有关即插即用设备树的详细信息，请参阅[设备树](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)。)每个 PnP 设备启动时，即插即用管理器枚举的子级的设备，如果有的话。 PnP 管理器配置子设备、 加载设备及其驱动程序，并启动设备。

    PnP 管理器加载每个设备驱动程序*而不考虑*的驱动程序的**StartType**， **LoadOrderGroup**，或者**依赖项**值。

    在此步骤中，即插即用管理器仅配置并启动设备可 PnP 枚举。 如果设备不是可 PnP 枚举，PnP 管理器将忽略设备，并且不会枚举其子项，即使子设备可 PnP 枚举。

5.  即插即用器负责加载并初始化服务类型的驱动程序\_系统\_尚未加载的开始。

    文件系统识别器 (FsRec) 是在这一次加载。 请注意，尽管它是在"启动文件系统"加载顺序组，但 FsRec 不启动文件系统。 实际的引导文件系统 − 引导过程开始时，它是加载已装入的引导卷 − 文件系统。

    在服务中更高版本\_系统\_加载开始阶段，在"文件系统"加载顺序组中的文件系统。 这包括名为管道文件系统 (NPFS) 和邮件槽文件系统 (MSFS)。 它不包括基于介质的文件系统，如 NTFS、 FAT、 CDFS 或 UDF。

    网络文件系统，位于"网络"加载顺序组，还加载在此阶段中。

6.  在启动时加载的所有驱动程序已初始化后，I/O 管理器调用将它们的任何驱动程序的重新初始化例程。 一个*重新初始化例程*由启动的驱动程序需要被授予其他已注册的回调例程处理时间此时在启动过程中的。 通过调用注册要重新初始化例程[ **IoRegisterBootDriverReinitialization** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioregisterbootdriverreinitialization)或[ **IoRegisterDriverReinitialization** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioregisterdriverreinitialization).

7.  服务控制管理器加载服务类型的驱动程序\_自动\_尚未加载的开始。

### <a name="span-idddkfilesystemrecognizerifspanspan-idddkfilesystemrecognizerifspanfile-system-recognizer"></a><span id="ddk_file_system_recognizer_if"></span><span id="DDK_FILE_SYSTEM_RECOGNIZER_IF"></span>文件系统识别器

在系统启动之后，附加到系统的所有卷的存储设备驱动程序加载和启动。 但是，并非所有内置的文件系统已加载，并且不是所有文件系统卷。 文件系统识别器 (FsRec) 执行这些任务，根据需要来处理[ **IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)请求。

在服务中加载 FsRec\_系统\_系统启动的启动阶段。 请注意，尽管它是在"启动文件系统"加载顺序组，但 FsRec 不启动文件系统。 实际的引导文件系统 − 引导过程开始时，它是加载已装入的引导卷 − 文件系统。

 

 




