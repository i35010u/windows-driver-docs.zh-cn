---
title: 存储卷
description: 存储卷
ms.assetid: 37b65bb6-7c62-47be-a16d-3813dc4c1259
keywords:
- 筛选器驱动程序 WDK 文件系统，存储卷
- 文件系统筛选器驱动程序 WDK，存储卷
- 存储卷 WDK 文件系统
- 计数管理器 WDK 文件系统
- 存储设备对象 WDK 文件系统
- 文件系统中，参数块卷 WDK
- VPBs WDK 文件系统
- 文件系统中的，有关存储卷的卷 WDK
- WDK 的逻辑卷文件系统
- 分区 WDK 文件系统
- 唯一的卷名称 WDK 文件系统
- Guid WDK 文件系统
- 名称 WDK 文件系统
- 唯一的卷名称
- DFS-R：
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33aa59f884e99a17349c2c73a66dd404553de677
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564764"
---
# <a name="storage-volumes"></a>存储卷


## <span id="ddk_storage_volumes_if"></span><span id="DDK_STORAGE_VOLUMES_IF"></span>


一个*卷*是存储设备，如固定的磁盘、 软盘、 CD-ROM、 格式设置为存储目录和文件。 一个较大卷可以分为多个*逻辑卷*，也称为*分区*。 由特定的基于介质的文件系统，如 NTFS、 FAT 或 CDFS 格式使用每个逻辑卷。

一个*存储卷*，或*存储设备对象*，通常表示逻辑卷到系统的物理设备对象 (PDO) − 是 − 的设备对象。 存储设备对象驻留在存储设备堆栈，但它不一定是堆栈中的最顶层的设备对象。

存储卷是已装入文件系统，它会创建一个文件系统卷设备对象 (VDO) 用于表示文件系统卷。 文件系统，通过调用共享对象存储设备对象装载 VDO*卷参数块*(VPB)。

### <a name="span-idddkmountmanagerifspanspan-idddkmountmanagerifspanmount-manager"></a><span id="ddk_mount_manager_if"></span><span id="DDK_MOUNT_MANAGER_IF"></span>计数管理器

*计数管理器*是负责管理存储卷的信息，例如卷名称、 驱动器号和卷装入点 I/O 系统的一部分。 当新的存储卷添加到系统中时，计数管理器将通知的以下两种方式在其到达：

-   创建存储卷调用的类驱动程序[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506) MOUNTDEV 中注册一个新接口\_已装载\_设备\_GUID 接口类。 在此情况下，插设备接口通知机制在系统中的警报计数管理器的卷的到达。

-   存储卷的驱动程序将计数管理器发送 IRP\_MJ\_设备\_控制请求指定[ **IOCTL\_MOUNTMGR\_卷\_到达\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff560477)对 i/o 控制代码。 可以通过调用创建此请求[ **IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)。

### <a name="span-idddkuniquevolumenameifspanspan-idddkuniquevolumenameifspanunique-volume-name"></a><span id="ddk_unique_volume_name_if"></span><span id="DDK_UNIQUE_VOLUME_NAME_IF"></span>唯一的卷名称

装入管理器响应到达新的存储卷通过查询卷驱动程序的以下信息：

-   卷的非持久性设备对象名称 （或目标名称），位于**设备**系统对象树的目录 (例如："\\设备\\HarddiskVolume1")

-   卷的全局唯一标识符，(GUID)，也称为*唯一卷名称*

-   该卷，例如驱动器号的建议持续性的符号链接名称 (例如，"\\DosDevices\\d:")

有关存储驱动程序和装入管理器之间的交互的详细信息，请参阅[存储类驱动程序中支持装入管理器请求](https://msdn.microsoft.com/library/windows/hardware/ff567603)。

 

 




