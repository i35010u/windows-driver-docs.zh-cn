---
title: IEEE 1394 控制器的设备对象示例
description: IEEE 1394 控制器的设备对象示例
ms.assetid: 9a83786b-8821-43b7-bf86-c85f2dcb9749
keywords:
- 存储驱动程序 WDK，设备对象
- 设备对象 WDK 存储
- IEEE 1394 控制器示例 WDK 存储
- PCI IEEE 1394 控制器示例 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77a6f784544a26f8a37010986f0f6d2fd9e23fc8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331725"
---
# <a name="device-object-example-for-an-ieee-1394-controller"></a>IEEE 1394 控制器的设备对象示例


## <span id="ddk_device_object_example_for_an_ieee_1394_controller_kg"></span><span id="DDK_DEVICE_OBJECT_EXAMPLE_FOR_AN_IEEE_1394_CONTROLLER_KG"></span>


下图显示了为与使用 IEEE 1394 CD-ROM 附加 PCI IEEE 1394 控制器的系统创建的设备对象。 连接到 SCSI 适配器的设备的设备对象中所述[SCSI HBA 的设备对象示例](device-object-example-for-a-scsi-hba.md)。

![为与使用 IEEE 1394 CD-ROM 附加 PCI IEEE 1394 控制器的系统创建的设备对象](images/kg201-3.png)

设备对象树的 IEEE 1394 控制器上的 CD-ROM 设备

从图底部开始，下面描述了每个设备对象和其相应的驱动程序：

1.  从存储总线 FDO 最多适配器 PDOs 设备树的说明，请参阅[SCSI HBA 的设备对象示例](device-object-example-for-a-scsi-hba.md)。

2.  IEEE 1394 驱动程序堆栈中的最高驱动程序创建 SBP2 磁盘设备 PDO。 IEEE 1394 驱动程序堆栈最终向目标 CD-ROM 设备上的 IEEE 1394 总线发出 SBP2 命令。

3.  作为创建筛选器执行操作，并将其附加到 SBP2 磁盘设备 PDO 的筛选器驱动程序实现的系统提供的 IEEE 1394 存储端口驱动程序。 IEEE 1394 存储端口驱动程序将从 CD-ROM 类驱动程序 Srb 转换为其颁发给基础的 IEEE 1394 驱动程序堆栈 SBP2 命令。 此驱动程序提供下一步低存储驱动程序的接口是与呈现 SCSI 端口/微型端口驱动程序中所述的相同[SCSI HBA 的设备对象示例](device-object-example-for-a-scsi-hba.md)。

4.  CD-ROM 类驱动程序创建 FDO 并附加到下一步下一个设备对象，它是任一 SBP2 端口筛选器执行操作或另一个筛选器通过附加到堆栈干预的筛选器驱动程序。 类驱动程序通过较低的驱动程序的设备对象向设备发出的所有后续请求。

 

 




