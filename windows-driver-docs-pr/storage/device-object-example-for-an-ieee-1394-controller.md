---
title: IEEE 1394 控制器的设备对象示例
description: IEEE 1394 控制器的设备对象示例
keywords:
- 存储驱动程序 WDK，设备对象
- 设备对象 WDK 存储
- IEEE 1394 控制器示例 WDK 存储
- PCI IEEE 1394 控制器示例 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b60019344816e9d1504216a6b86b6c9fcc4377a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835333"
---
# <a name="device-object-example-for-an-ieee-1394-controller"></a>IEEE 1394 控制器的设备对象示例


## <span id="ddk_device_object_example_for_an_ieee_1394_controller_kg"></span><span id="DDK_DEVICE_OBJECT_EXAMPLE_FOR_AN_IEEE_1394_CONTROLLER_KG"></span>


下图显示了为系统创建的设备对象，这些对象具有附加了 IEEE 1394 CD-ROM 的 PCI IEEE 1394 控制器。 [SCSI HBA 的设备对象示例](device-object-example-for-a-scsi-hba.md)中介绍了附加到 scsi 适配器的设备的设备对象。

![为系统创建的设备对象，其 PCI IEEE 1394 控制器附带了 IEEE 1394 CD-ROM](images/kg201-3.png)

IEEE 1394 控制器上 cd-rom 设备的设备对象树

从图的底部开始，下面介绍了每个设备对象及其相应的驱动程序：

1.  有关从存储总线 FDO 到适配器 PDOs 的设备树的说明，请参阅 [SCSI HBA 的设备对象示例](device-object-example-for-a-scsi-hba.md)。

2.  IEEE 1394 驱动程序堆栈中的最高驱动程序创建 SBP2 磁盘设备 PDO。 IEEE 1394 驱动程序堆栈最终会向 IEEE 1394 总线上的目标 CD-ROM 设备发出 SBP2 命令。

3.  系统提供的 IEEE 1394 存储端口驱动程序实现为创建筛选器的筛选器驱动程序，并将其附加到 SBP2 磁盘设备 PDO。 IEEE 1394 存储端口驱动程序将 CD-ROM 类驱动程序中的 SRBs 转换为颁发给基础 IEEE 1394 驱动程序堆栈的 SBP2 命令。 此驱动程序提供给下一个较低存储驱动程序的接口与 scsi [HBA 设备对象示例](device-object-example-for-a-scsi-hba.md)中所述的 scsi 端口/微型端口驱动程序所示的接口相同。

4.  Cd-rom 类驱动程序将创建一个 FDO，并将其附加到下一个较低的设备对象，该对象是 SBP2 端口筛选器或其他筛选器通过干预筛选器驱动程序连接到堆栈。 类驱动程序通过低级驱动程序的设备对象发出对设备的所有后续请求。

 

 




