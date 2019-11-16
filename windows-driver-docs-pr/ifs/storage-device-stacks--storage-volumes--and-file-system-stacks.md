---
title: 存储设备堆栈、存储卷和文件系统堆栈
description: 存储设备堆栈、存储卷和文件系统堆栈
ms.assetid: 5240ce9b-acfa-4e9c-9962-bc776878827c
keywords:
- 存储设备 WDK 文件系统
- 堆栈 WDK 文件系统
- 设备对象 WDK 文件系统
- 卷 WDK 文件系统
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1a111ba12590df0bd9be2619fe7a905e9a927fd2
ms.sourcegitcommit: 2a1c24db881ed843498001493c3ce202c9aa03f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/16/2019
ms.locfileid: "74128453"
---
# <a name="storage-device-stacks-storage-volumes-and-file-system-stacks"></a>存储设备堆栈、存储卷和文件系统堆栈

> [!NOTE]
> 为了获得最佳的可靠性和性能，请使用[文件系统筛选器驱动程序](filter-manager-and-minifilter-driver-architecture.md)，而不是旧的文件系统筛选器驱动程序 若要将旧驱动程序移植到微筛选器驱动程序，请参阅[迁移旧筛选器驱动程序的准则](guidelines-for-porting-legacy-filter-drivers.md)。

在探索文件系统旧筛选器驱动程序如何附加到文件系统和卷之前，必须了解存储设备堆栈、存储卷和文件系统堆栈之间的关系。

## <a name="storage-device-stacks"></a>存储设备堆栈

大多数存储驱动程序都是 pnp 设备驱动程序，由 PnP 管理器加载并管理。 存储设备表示为计算机上的每个物理或逻辑设备包含一个设备节点或*devnode*的 PnP*设备树*。 请务必注意，文件系统和文件系统筛选器驱动程序不是 PnP 设备驱动程序;因此 PnP[设备树]((https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree))不包含它们的 devnodes。

特定存储设备的 devnode 包含设备的*存储设备堆栈*;这是表示设备的存储设备驱动程序的附加设备对象的链。 由于存储设备（如磁盘）可能包含一个或多个逻辑卷（分区或动态卷），因此存储设备堆栈本身通常与堆栈更类似于树。 此树的根是存储适配器或与存储堆栈集成的其他设备堆栈的功能设备对象（FDO）。 此树的叶是逻辑卷（也称为*存储卷*）的物理设备对象（PDOs），可以在其中装入文件系统卷。

有关某些典型存储设备堆栈的关系图和说明，请参阅存储设备设计指南的以下部分：

- [SCSI HBA 的设备对象示例](https://docs.microsoft.com/windows-hardware/drivers/storage/device-object-example-for-a-scsi-hba)

- [IEEE 1394 控制器的设备对象示例](https://docs.microsoft.com/windows-hardware/drivers/storage/device-object-example-for-an-ieee-1394-controller)

## <a name="storage-volumes"></a>存储卷

*卷*是格式化为存储目录和文件的存储设备，例如固定磁盘、软盘或 cd-rom。 大型卷可以分为多个*逻辑卷*（也称为*分区*）。 每个逻辑卷的格式由特定的基于媒体的文件系统（例如 NTFS、FAT 或 CDFS）使用。

*存储卷*或*存储设备对象*是一个设备对象−，通常是表示系统的逻辑卷的物理设备对象（PDO）−。 存储设备对象驻留在存储设备堆栈中，但它不一定是堆栈中最顶层的设备对象。

在存储卷上装载文件系统时，它会创建文件系统卷设备对象（VDO），以将卷表示给文件系统。 文件系统 VDO 通过名为*volume 参数块*（VPB）的共享对象，装载到存储设备对象上。

### <a name="mount-manager"></a>装载管理器

*装载管理器*是 i/o 系统的一部分，负责管理存储卷信息，例如卷名称、驱动器号和卷装入点。 向系统中添加新的存储卷时，将通过以下任一方式向装载管理器通知其到达：

- 创建存储卷的类驱动程序调用[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)来注册 MOUNTDEV_MOUNTED_DEVICE_GUID 接口类中的新接口。 发生这种情况时，即插即用设备接口通知机制会向装入管理器发出卷在系统中的到达的警报。

- 存储卷的驱动程序向装入管理器发送 IRP_MJ_DEVICE_CONTROL 请求，并指定 i/o 控制代码[**IOCTL_MOUNTMGR_VOLUME_ARRIVAL_NOTIFICATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mountmgr/ni-mountmgr-ioctl_mountmgr_volume_arrival_notification) 。 可以通过调用[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)来创建此请求。

### <a name="unique-volume-name"></a>唯一卷名

装载管理器通过查询卷驱动程序来响应新存储卷的到达，以获取以下信息：

- 位于系统对象树的**设备**目录中的卷的非持久性设备对象名称（或目标名称）（例如： "\Device\HarddiskVolume1"）

- 卷的全局唯一标识符（GUID），也称为*唯一卷名*

- 卷的建议持久符号链接名称，如驱动器号（例如，"\DosDevices\D："）

有关存储驱动程序与装载管理器之间的交互的详细信息，请参阅[在存储类驱动程序中支持装入管理器请求](https://docs.microsoft.com/windows-hardware/drivers/storage/supporting-mount-manager-requests-in-a-storage-class-driver)。

## <a name="file-system-stacks"></a>文件系统堆栈

文件系统驱动程序创建两种不同类型的设备对象：控制设备对象（CDO）和卷设备对象（VDO）。 *文件系统堆栈*包含其中一个设备对象，以及附加到它的文件系统筛选器驱动程序的任何筛选器设备对象。 文件系统的设备对象始终构成堆栈的底部。

### <a name="file-system-cdos"></a>文件系统 CDOs

文件系统 CDOs 表示整个文件系统，而不是单个卷，存储在全局文件系统队列中。 文件系统会在其**DriverEntry**例程中创建一个或多个命名 CDOs。 例如，FastFat 创建两个 CDOs：一个用于固定介质，另一个用于可移动介质。 CDFS 只创建一个 CDO，因为它只有可移动介质。

需要为文件系统 CDOs 命名。 这是因为文件系统筛选器驱动程序以及许多内核模式支持例程依赖于 VDOs 和 CDOs 之间的这一区别来区分它们。

### <a name="file-system-vdos"></a>文件系统 VDOs

文件系统 VDOs 表示由文件系统装载的卷。 文件系统在装入卷时创建 VDO，通常是为了响应卷装入请求。 与 CDO 不同，VDO 始终与特定的逻辑或物理存储设备相关联。

> [!NOTE]
> 与 CDOs 不同，VDOs 永远不能命名，因为命名卷设备对象会创建安全漏洞。
