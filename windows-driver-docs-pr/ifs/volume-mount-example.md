---
title: 卷装载示例
description: 卷装载示例
ms.assetid: d6645d05-a945-4454-ac7c-122219bbdc50
keywords:
- 筛选器驱动程序 WDK 文件系统，卷装入过程
- 文件系统筛选器驱动程序 WDK，卷装入过程
- 装载卷 WDK 文件系统
- 卷 WDK 文件系统，装载
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 9d66e976134eb96690ef3db760dd7534ac1352c8
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910447"
---
# <a name="volume-mount-example"></a>卷装载示例

> [!NOTE]
> 为了获得最佳的可靠性和性能，请使用带有筛选器管理器支持的[文件系统微筛选器驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-concepts)，而不是使用旧的文件系统 若要将旧驱动程序移植到微筛选器驱动程序，请参阅[迁移旧筛选器驱动程序的准则](guidelines-for-porting-legacy-filter-drivers.md)。

下图显示了在装入任何卷之前，CDFS 可能的外观。 在此示例中，两个筛选器已附加到 CDFS 控制设备对象。 （注意：不显示包含 CDFS control 设备对象的全局文件系统队列。）

![在卷装入前说明 cdfs 的关系图](images/cdfsunmounted.png)

下图显示了尚未装载为 CDFS 卷的 CD-ROM 存储设备的典型驱动程序堆栈。

![说明在卷装入前 cd-rom 存储设备堆栈的示意图](images/cdromstack.png)

下图显示了 CDFS 文件系统在 CD-ROM 设备上装入卷后，文件系统驱动程序堆栈、卷堆栈和 cd-rom 存储设备堆栈的外观。

![说明装入的 cdfs 卷的关系图](images/cdfsmountedstacks.png)

有关上图的一些注释：

- CDFS 控件设备对象构成了文件系统驱动程序堆栈的基础。 此堆栈未装载到存储设备上，可以直接接收 Irp，还可以包含文件系统筛选器设备对象。 筛选器附加到文件系统控制设备对象以监视卷装入（[**IRP_MJ_FILE_SYSTEM_CONTROL**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)、IRP_MN_MOUNT_VOLUME）请求。 需要为文件系统控制设备对象命名。 这可以将它们与从不命名的文件系统卷设备对象区分开来。

- 如图所示，尽管装载 CDFS 卷后，可以将第二个存储筛选器附加到 CD-ROM 存储设备堆栈的顶部，但此筛选器将不会从文件系统堆栈向下传递的任何 Irp 发送到存储 d设备堆栈。 但是，它会收到直接发送到存储设备堆栈的任何 Irp。

- 请务必注意，在文件系统已装入卷后，存储设备堆栈仍可以直接接收 Irp。 具体而言，电源 Irp （IRP_MJ_POWER）始终直接发送到存储设备堆栈，从不发送到文件系统堆栈。 （因此，文件系统筛选器驱动程序不应在其**DriverEntry**例程中注册 IRP_MJ_POWER 的调度例程。）

  但是，可以将 PnP Irp （[**IRP_MJ_PNP**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-pnp)）发送到任一堆栈。 默认情况下，在文件系统卷上链接的筛选器驱动程序应始终将这些 Irp 传递到下一个较低的驱动程序，以便文件系统的卷设备可以将 Irp 向下传递到存储设备堆栈。
