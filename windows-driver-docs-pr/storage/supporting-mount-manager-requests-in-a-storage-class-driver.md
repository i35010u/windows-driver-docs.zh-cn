---
title: 支持存储类驱动程序中的装入管理器请求
description: 支持存储类驱动程序中的装入管理器请求
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
ms.openlocfilehash: 0c1b4a5a9b64e42814d383ee742791ce9967a901
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820511"
---
# <a name="supporting-mount-manager-requests-in-a-storage-class-driver"></a>支持存储类驱动程序中的装入管理器请求


## <span id="ddk_supporting_mount_manager_requests_in_a_storage_class_driver_kg"></span><span id="DDK_SUPPORTING_MOUNT_MANAGER_REQUESTS_IN_A_STORAGE_CLASS_DRIVER_KG"></span>


装入管理器 (MM) 负责管理卷名。 对于每个卷，它存储一个唯一的名称，并使用该卷永久标识，即使已从系统中删除该卷也是如此。 它还管理较少的永久性名称（如驱动器号），这些名称在重新启动时保持不变，但在系统中添加或删除卷时，它们的分配可能会改变。

装载管理器通过创建指向卷的设备对象的符号链接，为系统中的每个卷提供唯一的接口。 由于符号链接本身及其目标设备对象在系统重新启动时不会持久保存，因此，装载管理器会在注册表中的 *持久性名称数据库* 中保留符号链接的 *名称*。

此符号链接名称称为唯一的 *卷名*。 与传统的卷标签类似，当系统重新启动时，它会保持不变，但与卷标签不同，它是唯一的。 唯一卷名的格式为：

"**\\??\\卷 {**<em>GUID</em>**} \\**

其中 *GUID* 是标识卷的全局唯一标识符。

装载管理器的永久名称数据库位于注册表 (**HKLM/system/MountedDevices**) 的系统配置单元的 **MountedDevices** 注册表项中。 除了唯一的卷名称外，装载管理器还会将 *装入点* 名称存储在其永久性名称数据库中。 装入点名称可以进一步细分为两个类别： Win32 样式路径名，用作已装载卷的文件系统的根目录和驱动器号。

数据库中的每个永久性符号链接名称显示为 " **MountedDevices** " 项下的注册表值的名称，并且带有 *唯一 ID*。 唯一 ID 是卷的另一个唯一标识符， (不同于) 的唯一卷名。 它有助于识别可能有很多永久性符号链接名称引用相同的卷。

例如，单个卷的卷名为 <strong>" \\ \\ ？ \\Volume {</strong>7603f260-142a-11d4-ac67-806d6172696f **} \\ "** 可能具有伴随的驱动器号" \\ DosDevices \\ D： "和两个装入点" \\ DosDevices \\ C： \\ mymount "和" \\ DosDevices \\ E： \\ FilesysD \\ mnt "。 这会在安装管理器的永久符号链接名称数据库中生成四个条目：一个用于唯一的卷名称，一个用于驱动器号，两个用于两个装入点名称。 所有这四个条目共享相同的唯一 id。因此查看 **MountedDevices** 注册表项的用户能够检测到所有四个永久性名称都指向同一卷。

以下 acreen 快照说明了如何在 **MountedDevices** 注册表项中显示永久名称。

![说明永久性名称在 mounteddevices 注册表项中的显示方式的屏幕截图](images/mntmgr.png)

装载管理器依靠即插即用设备接口通知机制来向其发出卷到达和删除警报。 因此，每个客户端 (即每个卷驱动程序，通常是类驱动程序) 必须 \_ 通过调用 IoRegisterDeviceInterface 在 MOUNTDEV 装入的设备 GUID 接口类中创建一个接口， \_ \_ 以在它所管理的卷的系统中通知到达的安装管理器。 [**IoRegisterDeviceInterface**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface) MOUNTDEV \_ 装入的 \_ 设备 \_ GUID 接口类 guid 在 *mountmgr* 中定义。

接收到卷接口到达即插即用通知时，装载管理器会向客户端发送三个设备控制 Irp：

* [**IOCTL \_ MOUNTDEV \_ 查询 \_ 设备 \_ 名称**](/windows-hardware/drivers/ddi/mountmgr/ni-mountmgr-ioctl_mountdev_query_device_name)
* [**IOCTL \_ MOUNTDEV \_ 查询 \_ 唯一 \_ ID**](/windows-hardware/drivers/ddi/mountdev/ni-mountdev-ioctl_mountdev_query_unique_id)
* [**IOCTL \_ MOUNTDEV \_ 查询 \_ 建议的 \_ 链接 \_ 名称**](/windows-hardware/drivers/ddi/mountdev/ni-mountdev-ioctl_mountdev_query_suggested_link_name)

为了响应这三个 IOCTLs，客户端应在系统对象树的 **设备** 目录中返回卷的非持久性设备对象名称 (或目标名称)  (例如： " \\ device \\ HarddiskVolume1" ) 、唯一卷 ID 和卷的建议永久符号链接名称。 尽管客户端可以选择忽略 [**ioctl \_ MOUNTDEV \_ 查询 \_ 建议的 \_ 链接 \_ 名称**](/windows-hardware/drivers/ddi/mountdev/ni-mountdev-ioctl_mountdev_query_suggested_link_name)，但在接收 [**ioctl \_ MOUNTDEV \_ 查询 \_ 设备 \_ 名称**](/windows-hardware/drivers/ddi/mountmgr/ni-mountmgr-ioctl_mountdev_query_device_name) 或 IOCTL \_ MOUNTDEV \_ 查询 \_ 唯一 \_ ID 时，它们需要提供唯一的卷 ID。 装载管理器完全依赖于客户端提供唯一的卷 ID，如果客户端不提供，则装载管理器无法将装入点（例如驱动器号）分配给卷。

有关这些 IOCTLs 的详细信息，请参阅 [由装载管理器发送的 I/o 控制代码](/windows-hardware/drivers/ddi/index)。

如果客户端向装入管理器通知其卷的到达，但在查询时无法为卷提供唯一的 ID，则会将该卷置于 *死安装设备* 列表中。 出现这种情况时，客户端可以向装载管理器发送 [**ioctl \_ MOUNTMGR \_ 检查 \_ \_**](/windows-hardware/drivers/ddi/mountmgr/ni-mountmgr-ioctl_mountmgr_check_unprocessed_volumes) 未处理的卷 IOCTL，请求装载管理器重新扫描其已安装的设备列表，并再次尝试在列表中查询客户端各自卷的唯一 id。 有关 IOCTL \_ MOUNTMGR Xxx IOCTLs 的详细信息 \_ ，请参阅 [由装载管理器客户端发送的 i/o 控制代码](/windows-hardware/drivers/ddi/index)

在装载管理器收到新引入的卷的唯一卷 ID 后，它会在其数据库中搜索分配给该唯一 ID 的所有永久名称，并为每个永久性符号链接名称创建卷的符号链接。

当装载管理器检测到某个卷已脱机时，它将删除指向该设备对象的符号链接，而不会删除装载管理器数据库中相应的符号链接名称。

有关装载管理器客户端如何创建永久性符号名称的信息，请参阅 [**IOCTL \_ MOUNTMGR \_ 创建 \_ 点**](/windows-hardware/drivers/ddi/mountmgr/ni-mountmgr-ioctl_mountmgr_create_point)。

 

