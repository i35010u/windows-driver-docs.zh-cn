---
title: PCI IDE 控制器的设备对象示例
description: PCI IDE 控制器的设备对象示例
ms.assetid: 7cb97da7-1d94-42a1-af3a-9085e68c8f28
keywords:
- 存储驱动程序 WDK，设备对象
- 设备对象 WDK 存储
- PCI IDE 控制器示例 WDK 存储
- IDE 控制器 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28748d270a4b8d06b8d4c7a65ea683546626b01d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331734"
---
# <a name="device-object-example-for-a-pci-ide-controller"></a>PCI IDE 控制器的设备对象示例


## <span id="ddk_device_object_example_for_a_pci_ide_controller_kg"></span><span id="DDK_DEVICE_OBJECT_EXAMPLE_FOR_A_PCI_IDE_CONTROLLER_KG"></span>


下图显示了为使用具有两个 IDE 磁盘附加到一个通道和 IDE CD-ROM 的 PCI IDE 控制器的系统创建的设备对象附加到其他。

![为使用具有两个 IDE 磁盘附加到一个通道，并附加到其他 IDE CD-ROM 的 PCI IDE 控制器的系统创建的设备对象](images/kg201-4.png)

CD-ROM 和 IDE 控制器上的磁盘设备的设备对象树

从图底部开始，下面描述了每个设备对象和其关联的驱动程序：

1.  PCI 总线驱动程序创建 PCI 总线 FDO，并将其附加到 PCI 总线 PDO 已通过即插即用管理器 （不在此图中所示）。

2.  PCI 总线驱动程序枚举适配器和其总线，包括所有 IDE 控制器上的控制器，并创建每个 PDO。

3.  IDE 控制器驱动程序，以及其 IDE 控制器微型驱动程序，创建 FDO，并将其附加到的控制器 PDO。

4.  IDE 控制器驱动程序"枚举"控制器的通道。 实际上，这意味着它将创建两个 PDOs，一个用于每个控制器的通道，并且它会将附加两者通道 PDOs 到控制器 FDO。

5.  IDE 通道驱动程序创建 FDO，并将其附加到的是 PDO 通道。

6.  IDE 通道驱动程序枚举其通道上的设备，并创建每个设备 PDO。 图显示一个设备对象树，用于在 IEEE 1394 控制器上的 CD-ROM 设备说明了三个 IDE 通道驱动程序创建此类 PDOs： 所创建的控制器的第一个通道，通道驱动程序的两个硬盘驱动器 PDOs 和已创建的控制器的第二个通道的通道驱动程序的 CD-ROM PDO。

7.  磁盘类驱动程序创建 FDO，并将其附加到相关联的磁盘 PDO，完全一样 SCSI，并创建 FDO CD-ROM 驱动程序，并将其附加到相关联的 CD-ROM PDO。 如下所示 SCSI 的情况下，筛选器驱动程序执行操作可以插入设备 PDO 和设备 FDO 之间。 IEEE 1394 控制器上显示 CD-ROM 设备的设备对象树图说明了此使用 CD 音频筛选器执行此操作可以选择放在 CD-ROM PDO 的正上方。

 

 




