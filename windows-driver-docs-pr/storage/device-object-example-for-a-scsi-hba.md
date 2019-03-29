---
title: SCSI HBA 的设备对象示例
description: SCSI HBA 的设备对象示例
ms.assetid: 695ccf9a-a18f-4f1f-bfdc-24fefc2846b4
keywords:
- 存储驱动程序 WDK，设备对象
- 设备对象 WDK 存储
- SCSI HBA 设备对象示例 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31bd35a38ec4a4707914335d1e1c3c480e02a0ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576367"
---
# <a name="device-object-example-for-a-scsi-hba"></a>SCSI HBA 的设备对象示例


## <span id="ddk_device_object_example_for_a_scsi_hba_kg"></span><span id="DDK_DEVICE_OBJECT_EXAMPLE_FOR_A_SCSI_HBA_KG"></span>


下图显示了为与 PCI IEEE 1394 控制器的系统和使用 CD-ROM 和附加的分区的磁盘设备的 PCI SCSI 适配器创建的设备对象。 对象的设备连接到 IEEE 1394 控制器进行显示和中所述[IEEE 1394 控制器的设备对象示例](device-object-example-for-an-ieee-1394-controller.md)。

![为与 PCI IEEE 1394 控制器的系统和使用 CD-ROM 和附加的分区的磁盘设备的 PCI SCSI 适配器创建的设备对象](images/kg201-2.png)

CD-ROM 和 SCSI HBA 上的磁盘设备的设备对象树

从图底部开始，下面描述了每个设备对象和其关联的驱动程序：

1.  存储总线驱动程序创建的存储总线 FDO，并将其附加到存储总线 PDO 创建的 （不在此图中所示） 的即插即用管理器。 存储总线 FDO 下面的设备对象树的结构取决于存储总线和如何集成到系统。 端口驱动程序级别以上的存储驱动程序不使用任何这些较低的对象进行交互。

    此图显示了存储总线 FDO 创建的包含 PCI 总线的系统的 PCI 总线驱动程序。

2.  PCI 总线驱动程序枚举，并在其总线上创建的每个存储适配器 PDO。 相应的存储端口驱动程序创建 FDO，并将其附加到其适配器 PDO。

    此图显示了两个适配器 PDOs： 一个用于 IEEE 1394 控制器 (中所述[IEEE 1394 控制器的设备对象示例](device-object-example-for-an-ieee-1394-controller.md))，另一个用于 SCSI HBA。 SCSI 端口驱动程序和关联的微型端口驱动程序创建 FDO 并将其附加到 SCSI 适配器 PDO。

3.  存储端口驱动程序可通过创建每个目标设备连接到其适配器 PDO 虚拟化的目标设备。 此图显示了两个 SCSI 端口/微型端口驱动程序创建此类 PDOs： 一个用于硬盘磁盘驱动器，一个用于 CD-ROM。

4.  一个或多个筛选器驱动程序可以附加到目标设备 PDO 导出存储端口驱动程序的筛选设备对象 （筛选器执行操作）。 这样的筛选器驱动程序可以截获和 alter 发送的请求的类驱动程序到目标设备，例如，若要解决特定于设备的问题，而无需对泛型类或端口驱动程序的特定于硬件的更改。

    此图显示了筛选器通过 CD 音频筛选器驱动程序附加到 CD ROM 的 PDO。

5.  存储类驱动程序创建 FDO，并将其附加到下一步下一个设备对象，它是目标设备 PDO 导出存储端口驱动程序或筛选器附加到堆栈干预的筛选器驱动程序的执行操作。 类驱动程序将向通过较低的驱动程序的设备对象的存储设备发出的所有后续请求。

    此图显示了两个此类 FDOs： 一个表示 CD-ROM 设备，另一个表示分区 0 的硬盘驱动器。 分区 0 表示整个原始磁盘，并始终存在是否驱动器已进行分区。

6.  类驱动程序也可用作总线驱动程序，当 PnP 管理器将查询其子设备时，返回一系列 PDOs (IRP\_MN\_查询\_设备\_关系**BusRelations**). 例如，如可移动磁盘分区的媒体设备的驱动程序可能会返回一系列 PDOs 表示其分区。 更高级别的驱动程序附加到这些 PDOs FDOs。

    此图显示了三个此类 PDOs，每个元素表示其地址为目标设备的磁盘分区。

    对于固定磁盘分区管理器将附加到 FDO 表示分区 0 并处理所有分区代表的即插即用操作。 分区管理器的活动是透明的磁盘类驱动程序和任何上部级筛选器驱动程序。

7.  上面的类驱动程序，可以附加一个或多个筛选器驱动程序。 与较低的级别筛选器驱动程序，不同的上部级筛选器驱动程序截获 Irp 发送到的类驱动程序，并可以更改它们之前将其转发到下一步下一个设备对象。 筛选器驱动程序可以截获任何读/写请求和转换所需数据，以及定义其他 I/O 控制代码 (Ioctl)，例如，若要启用用户应用程序提供的密码或其他相关的信息。

    此图显示了筛选器通过磁盘加密筛选器驱动程序创建并附加到磁盘 PDO 为分区 1。

 

 




