---
title: SCSI HBA 的设备对象示例
description: SCSI HBA 的设备对象示例
keywords:
- 存储驱动程序 WDK，设备对象
- 设备对象 WDK 存储
- SCSI HBA 设备对象示例 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 682379e4ab1a57a4833654ff54ed764ceb095367
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835335"
---
# <a name="device-object-example-for-a-scsi-hba"></a>SCSI HBA 的设备对象示例


## <span id="ddk_device_object_example_for_a_scsi_hba_kg"></span><span id="DDK_DEVICE_OBJECT_EXAMPLE_FOR_A_SCSI_HBA_KG"></span>


下图显示了为系统创建的设备对象，这些对象是使用 PCI IEEE 1394 控制器和 PCI SCSI 适配器（附加了 cd-rom 和分区磁盘设备）创建的。 用于附加到 IEEE 1394 控制器的设备的对象在 [ieee 1394 控制器的设备对象示例](device-object-example-for-an-ieee-1394-controller.md)中进行了说明和说明。

![使用 PCI IEEE 1394 控制器和 PCI SCSI 适配器为系统创建的设备对象连接了 cd-rom 和分区磁盘设备](images/kg201-2.png)

SCSI HBA 上的 cd-rom 和磁盘设备的设备对象树

从图的底部开始，下面介绍了每个设备对象及其关联的驱动程序：

1.  存储总线驱动程序为存储总线创建 FDO，并将其附加到 PnP 管理器创建的存储总线 PDO 上 (此图) 中未显示。 存储总线 FDO 下的设备对象树的结构取决于存储总线以及它如何集成到系统中。 超出端口驱动程序级别的存储驱动程序不会与这些较低的对象进行交互。

    此图显示了使用 PCI 总线的系统的 PCI 总线驱动程序创建的存储总线 FDO。

2.  PCI 总线驱动程序为其总线上的每个存储适配器枚举并创建一个 PDO。 相应的存储端口驱动程序将创建 FDO，并将其附加到其适配器的 PDO。

    此图显示了两个适配器 PDOs：一个用于 1394 IEEE [1394 控制器) 的设备对象示例](device-object-example-for-an-ieee-1394-controller.md) 中所述 (，另一个用于 SCSI HBA。 SCSI 端口驱动程序和关联的微型端口驱动程序创建 FDO，并将其附加到 SCSI 适配器 PDO。

3.  存储端口驱动程序通过为每个连接到其适配器的目标设备创建一个 PDO 来虚拟化目标设备。 此图显示了由 SCSI 端口/微型端口驱动程序创建的两个 PDOs：一个用于硬盘驱动器，另一个用于 cd-rom。

4.  一个或多个筛选器驱动程序可以将筛选器设备对象 (filter DO) 连接到存储端口驱动程序导出的目标设备 PDO。 此类筛选器驱动程序可以截获类驱动程序发送给目标设备的请求并将其更改为目标设备，例如，用于处理特定于设备的问题，而无需对泛型类或端口驱动程序进行硬件特定的更改。

    下图显示了 CD 音频筛选器驱动程序附加到 cd-rom 的 PDO 的筛选器。

5.  存储类驱动程序将创建一个 FDO，并将其附加到下一个较低的设备对象，这是由存储端口驱动程序或筛选器通过干预筛选器驱动程序连接到堆栈的目标设备 PDO。 类驱动程序通过低级驱动程序的设备对象发出对存储设备的所有后续请求。

    此图显示了两个 FDOs：一个表示 CD-ROM 设备，另一个代表硬盘驱动器的分区0。 分区0表示整个原始磁盘，并且无论驱动器是否已分区，始终存在。

6.  类驱动程序还可以充当总线驱动程序，并在 PnP 管理器查询其子设备时返回 PDOs 列表， (IRP \_ MN \_ 查询 \_ 设备 \_ 关系与 **BusRelations**) 。 例如，分区媒体设备（如可移动磁盘）的驱动程序可能会返回表示其分区的 PDOs 的列表。 较高级别的驱动程序将 FDOs 附加到这些 PDOs。

    此图显示了三个 PDOs，每个都表示一个可作为目标设备进行寻址的磁盘分区。

    对于固定磁盘，分区管理器会附加到表示分区0的 FDO，并代表所有分区处理 PnP 操作。 分区管理器的活动对于磁盘类驱动程序和任何顶级筛选器驱动程序都是透明的。

7.  一个或多个筛选器驱动程序可以附加到类驱动程序之上。 与较低级别筛选器驱动程序不同，上层筛选器驱动程序会截获发送到类驱动程序的 Irp，并可以在将其转发到下一个较低的设备对象之前对其进行更改。 筛选器驱动程序可以拦截任何读/写请求并根据需要转换数据，还可以定义额外的 i/o 控制代码 (IOCTLs) ，例如，使用户应用程序能够提供密码或其他相关信息。

    此图显示了由磁盘加密筛选器驱动程序创建并附加到分区1的磁盘 PDO 的筛选器。

 

 




