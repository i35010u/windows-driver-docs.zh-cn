---
title: 支持多功能 PCI 设备
description: 支持多功能 PCI 设备
ms.assetid: 57cbbcdb-7201-4bf4-a2a0-e613607e4509
keywords:
- 多功能设备 WDK、 PCI
- PCI 多功能标准 WDK
- 功能的设备对象 WDK 的多功能设备
- FDOs WDK 多功能设备
- 物理设备对象 WDK 多功能设备
- PDOs WDK 多功能设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef845df16c6780d252bd0d90809829a3baab6668
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342323"
---
# <a name="supporting-multifunction-pci-devices"></a>支持多功能 PCI 设备





如果多功能 PCI 设备完全符合 PCI 多功能标准，PCI 总线驱动程序枚举各个函数。 PCI 总线驱动程序管理是驻留在单个设备位置的多个函数的事实。 系统的其余部分，各个函数独立设备一样运行。

一种基于 NT 的平台上的 PCI 多功能设备的供应商必须执行以下操作：

-   确保设备符合 PCI 多功能规范。

-   为设备的每个函数提供即插即用功能驱动程序。

    由于系统提供总线驱动程序处理的多功能语义，功能的驱动程序可以是相同的驱动程序，可在函数已打包为单个设备。

-   提供设备的每个函数的 INF 文件。

    INF 文件可以是可在函数已打包为单个设备的相同文件。 INF 文件不需要任何特殊的多功能语义。

例如下, 图显示了可能会为 ISDN 和调制解调器函数具有的多功能 PCI 设备创建的示例设备堆栈。

![说明其父枚举每个函数的多功能设备的设备堆栈的关系图](images/mf-indep.png)

上图中，而不是枚举的一个多功能设备中所示，PCI 驱动程序枚举两个子设备。 即插即用的管理器会将典型的设备，如每个子设备查找 INF 文件加载适当的驱动程序调用其 AddDevice 例程，依次类推，直到为每个设备创建设备堆栈。 PCI 驱动程序进行仲裁子设备的资源，并管理设备的任何其他多功能方面。 多功能卡供应商为 ISDN 和调制解调器设备提供功能的驱动程序和 Inf 就像它们是不同的设备。

图重点介绍的功能驱动程序和总线驱动程序的每个函数和其关联 FDO 和 PDO。 任何筛选器驱动程序 （和筛选器 DOs） 为简单起见，省略了。

 

 




