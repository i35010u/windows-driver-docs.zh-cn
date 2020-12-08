---
title: PCI IDE 控制器的设备对象示例
description: PCI IDE 控制器的设备对象示例
keywords:
- 存储驱动程序 WDK，设备对象
- 设备对象 WDK 存储
- PCI IDE 控制器示例 WDK 存储
- IDE 控制器 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df4e031917204281e47f6c480c9f820758ac1545
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804699"
---
# <a name="device-object-example-for-a-pci-ide-controller"></a>PCI IDE 控制器的设备对象示例


## <span id="ddk_device_object_example_for_a_pci_ide_controller_kg"></span><span id="DDK_DEVICE_OBJECT_EXAMPLE_FOR_A_PCI_IDE_CONTROLLER_KG"></span>


下图显示了使用 PCI IDE 控制器为系统创建的设备对象，其中有两个 IDE 磁盘连接到一个通道，而 IDE cd-rom 附加到另一个通道。

![使用 PCI IDE 控制器为系统创建的设备对象，其中有两个 IDE 磁盘连接到一个通道，而 IDE cd-rom 附加到另一个通道](images/kg201-4.png)

IDE 控制器上 cd-rom 和磁盘设备的设备对象树

从图的底部开始，下面介绍了每个设备对象及其关联的驱动程序：

1.  PCI 总线驱动程序为 PCI 总线创建 FDO，并将其附加到 PnP 管理器创建的 PCI 总线 PDO 上， (此图) 中未显示。

2.  PCI 总线驱动程序枚举其总线上的适配器和控制器（包括所有 IDE 控制器），并为每个控制器创建一个 PDO。

3.  IDE 控制器驱动程序及其 IDE 控制器微型驱动程序创建 FDO 并将其附加到控制器的 PDO。

4.  IDE 控制器驱动程序 "枚举" 控制器的通道。 实际上，这意味着它会创建两个 PDOs，一个用于控制器的通道，并将两个通道 PDOs 附加到控制器 FDO。

5.  IDE 通道驱动程序将创建 FDO，并将其附加到该通道的 PDO。

6.  IDE 通道驱动程序会枚举其通道上的设备，并为每个设备创建一个 PDO。 显示 IEEE 1394 控制器上 CD-ROM 设备的设备对象树的图演示了由 IDE 通道驱动程序创建的三个 PDOs：由通道驱动程序为控制器的第一个通道创建的两个硬盘驱动器，以及由控制器的第二个通道的通道驱动程序创建的 CD-ROM PDO。

7.  Disk 类驱动程序将创建一个 FDO，并将其附加到关联的磁盘 PDO 上（与使用 SCSI 时完全相同），CD-ROM 驱动程序将创建 FDO 并将其附加到关联的 CD-ROM PDO。 对于 SCSI，可以在设备 PDO 和设备 FDO 之间插入筛选器驱动程序。 显示 IEEE 1394 控制器上 CD-ROM 设备的设备对象树的图演示了这种使用 CD 音频筛选器的情况，可以选择性地将其置于 cd-rom PDO 上方。

 

 




