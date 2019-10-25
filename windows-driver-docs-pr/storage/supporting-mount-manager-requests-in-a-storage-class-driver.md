---
title: 支持存储类驱动程序中的装入管理器请求
description: 支持存储类驱动程序中的装入管理器请求
ms.assetid: fb37f862-70d6-4514-b481-16f664346422
keywords:
- 存储类驱动程序 WDK，装载管理器
- 类驱动程序 WDK 存储，装载管理器
- 装载管理器 WDK 存储
- MM WDK 存储
- 卷名称 WDK 存储
- 命名 WDK 存储
- 唯一卷名称 WDK 存储
- 持久名称数据库 WDK 存储
- MountedDevices
- 未装入设备的 WDK 存储
- 符号链接名称 WDK 存储
- 临时名称 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0a8b601638fe59e4b89f80f75539dbdf7ff5776
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844472"
---
# <a name="supporting-mount-manager-requests-in-a-storage-class-driver"></a>支持存储类驱动程序中的装入管理器请求


## <span id="ddk_supporting_mount_manager_requests_in_a_storage_class_driver_kg"></span><span id="DDK_SUPPORTING_MOUNT_MANAGER_REQUESTS_IN_A_STORAGE_CLASS_DRIVER_KG"></span>


装载管理器（MM）负责管理卷名。 对于每个卷，它存储一个唯一的名称，并使用该卷永久标识，即使已从系统中删除该卷也是如此。 它还管理较少的永久性名称（如驱动器号），这些名称在重新启动时保持不变，但在系统中添加或删除卷时，它们的分配可能会改变。

装载管理器通过创建指向卷的设备对象的符号链接，为系统中的每个卷提供唯一的接口。 由于符号链接本身及其目标设备对象在系统重新启动时不会持久保存，因此，装载管理器会在注册表中的*持久性名称数据库*中保留符号链接的*名称*。

此符号链接名称称为唯一的*卷名*。 与传统的卷标签类似，当系统重新启动时，它会保持不变，但与卷标签不同，它是唯一的。 唯一卷名的格式为：

" **\\？\\卷 {** <em>GUID</em> **}\\**

其中*GUID*是标识卷的全局唯一标识符。

装载管理器的永久名称数据库位于注册表系统配置单元（**HKLM/system/MountedDevices**）的**MountedDevices**注册表项中。 除了唯一的卷名称外，装载管理器还会将*装入点*名称存储在其永久性名称数据库中。 装入点名称可以进一步细分为两个类别： Win32 样式路径名，用作已装载卷的文件系统的根目录和驱动器号。

数据库中的每个永久性符号链接名称显示为 " **MountedDevices** " 项下的注册表值的名称，并且带有*唯一 ID*。 唯一 ID 是卷的另一个唯一标识符（与唯一卷名称不同）。 它有助于识别可能有很多永久性符号链接名称引用相同的卷。

例如，具有唯一卷名称 "\\\\的单个卷<strong>？\\Volume {</strong>7603f260-142a-11d4-ac67-806d6172696f **}\\"** 可能具有伴随的驱动器号"\\DosDevices\\D： "和两个装入点"\\DosDevices\\C：\\mymount "和"\\DosDevices\\E：\\FilesysD\\mnt "。 这会在安装管理器的永久符号链接名称数据库中生成四个条目：一个用于唯一的卷名称，一个用于驱动器号，两个用于两个装入点名称。 所有这四个条目共享相同的唯一 id。因此查看**MountedDevices**注册表项的用户能够检测到所有四个永久性名称都指向同一卷。

以下 acreen 快照说明了如何在**MountedDevices**注册表项中显示永久名称。

![说明永久性名称在 mounteddevices 注册表项中的显示方式的屏幕截图](images/mntmgr.png)

装载管理器依靠即插即用设备接口通知机制来向其发出卷到达和删除警报。 因此，每个客户端（即每个卷驱动程序，通常是类驱动程序）都必须通过调用[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface) ，在 MOUNTDEV\_\_装入的设备\_GUID 接口类，以便通知装载管理器它所管理的卷在系统中的到达量。 在*mountmgr*中定义了 MOUNTDEV\_装载\_设备\_guid 接口类 guid。

接收到卷接口到达即插即用通知时，装载管理器会向客户端发送三个设备控制 Irp：

* [**IOCTL\_MOUNTDEV\_查询\_设备\_名称**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mountmgr/ni-mountmgr-ioctl_mountdev_query_device_name)
* [**IOCTL\_MOUNTDEV\_查询\_唯一\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mountdev/ni-mountdev-ioctl_mountdev_query_unique_id)
* [**IOCTL\_MOUNTDEV\_查询\_建议的\_链接\_名称**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mountdev/ni-mountdev-ioctl_mountdev_query_suggested_link_name)

为了响应这三个 IOCTLs，客户端应返回位于系统对象树的**设备**目录中的卷的非持久性设备对象名称（或目标名称）（例如： "\\设备\\HarddiskVolume1"），唯一卷 ID 和卷的建议持久符号链接名称。 尽管客户端可以选择忽略[**ioctl\_MOUNTDEV\_QUERY\_建议的\_链接\_名称**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mountdev/ni-mountdev-ioctl_mountdev_query_suggested_link_name)，但在接收[**IOCTL\_MOUNTDEV\_查询时，需要提供唯一的卷 ID\_设备\_名称**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mountmgr/ni-mountmgr-ioctl_mountdev_query_device_name)或 IOCTL\_MOUNTDEV\_查询\_唯一的\_ID。 装载管理器完全依赖于客户端提供唯一的卷 ID，如果客户端不提供，则装载管理器无法将装入点（例如驱动器号）分配给卷。

有关这些 IOCTLs 的详细信息，请参阅[由装载管理器发送的 I/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

如果客户端向装入管理器通知其卷的到达，但在查询时无法为卷提供唯一的 ID，则会将该卷置于*死安装设备*列表中。 发生这种情况时，客户端可以向装载管理器发送[**IOCTL\_MOUNTMGR\_检查\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/mountmgr/ni-mountmgr-ioctl_mountmgr_check_unprocessed_volumes)未处理的\_卷 IOCTL，请求装载管理器重新扫描其已安装的设备列表，并再次尝试查询列表中客户端的唯一 Id。 有关 IOCTL\_MOUNTMGR\_xxx IOCTLs 的详细信息，请参阅[由装载管理器客户端发送的 I/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

在装载管理器收到新引入的卷的唯一卷 ID 后，它会在其数据库中搜索分配给该唯一 ID 的所有永久名称，并为每个永久性符号链接名称创建卷的符号链接。

当装载管理器检测到某个卷已脱机时，它将删除指向该设备对象的符号链接，而不会删除装载管理器数据库中相应的符号链接名称。

有关装载管理器客户端如何创建永久符号名称的信息，请参阅[**IOCTL\_MOUNTMGR\_创建\_点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mountmgr/ni-mountmgr-ioctl_mountmgr_create_point)。

 

 




