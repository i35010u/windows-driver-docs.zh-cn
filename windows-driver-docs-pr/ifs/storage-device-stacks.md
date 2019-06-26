---
title: 存储设备堆栈
description: 存储设备堆栈
ms.assetid: dc2c532d-4ec6-4c97-bb94-429dd06f7b7c
keywords:
- 筛选器驱动程序 WDK 文件系统，存储设备堆栈
- 文件系统筛选器驱动程序 WDK，存储设备堆栈
- 存储设备堆栈 WDK 文件系统
- 设备堆栈 WDK 文件系统
- 设备树 WDK 文件系统
- 即插即用设备树 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c02b4324a3ed0fc0c25666fe0c9ed06e11ce2000
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371316"
---
# <a name="storage-device-stacks"></a>存储设备堆栈


## <span id="ddk_storage_device_stacks_if"></span><span id="DDK_STORAGE_DEVICE_STACKS_IF"></span>


大多数存储驱动程序是即插即用设备驱动程序，加载和 PnP 管理器管理的。 存储设备都包含在 PnP*设备树*，其中包含一个设备节点中，或*devnode*，每个物理或逻辑设备在计算机上。 务必要注意的文件系统和文件系统筛选器驱动程序不是即插即用设备驱动程序;因此该即插即用设备树包含没有 devnodes 它们。 有关即插即用设备树的详细信息，请参阅[设备树](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)。

包含为某个特定存储设备 devnode*存储设备堆栈*对于设备; 这是表示设备的存储设备驱动程序的连接的设备对象的链。 由于存储设备，如磁盘、 可能包含一个或多个逻辑卷 （分区或动态卷），存储设备堆栈本身通常看起来更像树与一个堆栈。 此树的根是一个功能的设备对象 (FDO) 存储适配器或与存储堆栈集成的另一个设备堆栈。 此树的叶是物理设备对象 (PDO) 个逻辑卷，也称为存储卷<em>，</em>卷可以装载哪些文件系统上。

关系图和一些典型的存储设备堆栈的说明，请参阅存储设备设计指南的以下部分：

[对于 SCSI HBA 的设备对象示例](https://docs.microsoft.com/windows-hardware/drivers/storage/device-object-example-for-a-scsi-hba)

[IEEE 1394 控制器的设备对象示例](https://docs.microsoft.com/windows-hardware/drivers/storage/device-object-example-for-an-ieee-1394-controller)

 

 




