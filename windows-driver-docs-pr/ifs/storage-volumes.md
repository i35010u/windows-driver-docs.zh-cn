---
title: 存储卷
description: 存储卷
ms.assetid: 37b65bb6-7c62-47be-a16d-3813dc4c1259
keywords:
- 筛选器驱动程序 WDK 文件系统，存储卷
- 文件系统筛选器驱动程序 WDK，存储卷
- 存储卷 WDK 文件系统
- 装载管理器 WDK 文件系统
- 存储设备对象 WDK 文件系统
- 卷 WDK 文件系统，参数块
- VPBs WDK 文件系统
- 卷 WDK 文件系统，关于存储卷
- 逻辑卷 WDK 文件系统
- 分区 WDK 文件系统
- 唯一卷名称 WDK 文件系统
- Guid WDK 文件系统
- 命名 WDK 文件系统
- 唯一卷名
- 卷 GUID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61831f5ac31a28c0eb85c64c5fe607511621a5a9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840962"
---
# <a name="storage-volumes"></a>存储卷


## <span id="ddk_storage_volumes_if"></span><span id="DDK_STORAGE_VOLUMES_IF"></span>


*卷*是格式化为存储目录和文件的存储设备，例如固定磁盘、软盘或 cd-rom。 大型卷可以分为多个*逻辑卷*（也称为*分区*）。 每个逻辑卷的格式由特定的基于媒体的文件系统（例如 NTFS、FAT 或 CDFS）使用。

*存储卷*或*存储设备对象*是一个设备对象−，通常是表示系统的逻辑卷的物理设备对象（PDO）−。 存储设备对象驻留在存储设备堆栈中，但它不一定是堆栈中最顶层的设备对象。

在存储卷上装载文件系统时，它会创建文件系统卷设备对象（VDO），以将卷表示给文件系统。 文件系统 VDO 通过名为*volume 参数块*（VPB）的共享对象，装载到存储设备对象上。

### <a name="span-idddk_mount_manager_ifspanspan-idddk_mount_manager_ifspanmount-manager"></a><span id="ddk_mount_manager_if"></span><span id="DDK_MOUNT_MANAGER_IF"></span>装载管理器

*装载管理器*是 i/o 系统的一部分，负责管理存储卷信息，例如卷名称、驱动器号和卷装入点。 向系统中添加新的存储卷时，会通过以下任一方式向装载管理器通知其到达：

-   创建存储卷的类驱动程序会调用[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface) ，以便在装入\_设备\_GUID 接口类的 MOUNTDEV\_中注册新接口。 发生这种情况时，即插即用设备接口通知机制会向装入管理器发出卷在系统中的到达的警报。

-   用于存储卷的驱动程序将 IRP\_MJ\_设备\_控制请求，指定[**IOCTL\_MOUNTMGR\_卷\_到达**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mountmgr/ni-mountmgr-ioctl_mountmgr_volume_arrival_notification)i/o 控制代码的通知。 可以通过调用[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)来创建此请求。

### <a name="span-idddk_unique_volume_name_ifspanspan-idddk_unique_volume_name_ifspanunique-volume-name"></a><span id="ddk_unique_volume_name_if"></span><span id="DDK_UNIQUE_VOLUME_NAME_IF"></span>唯一卷名

装载管理器通过查询卷驱动程序来响应新存储卷的到达，以获取以下信息：

-   卷的非持久性设备对象名称（或目标名称）位于系统对象树的**设备**目录中（例如： "\\Device\\HarddiskVolume1"）

-   卷的全局唯一标识符（GUID），也称为*唯一卷名*

-   卷的建议持久符号链接名称，如驱动器号（例如，"\\DosDevices\\D："）

有关存储驱动程序与装载管理器之间的交互的详细信息，请参阅[在存储类驱动程序中支持装入管理器请求](https://docs.microsoft.com/windows-hardware/drivers/storage/supporting-mount-manager-requests-in-a-storage-class-driver)。

 

 




