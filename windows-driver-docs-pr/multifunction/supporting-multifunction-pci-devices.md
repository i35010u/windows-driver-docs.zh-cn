---
title: 支持多功能 PCI 设备
description: 支持多功能 PCI 设备
keywords:
- 多功能设备 WDK、PCI
- PCI 多功能标准版 WDK
- 功能设备对象 WDK 多功能设备
- FDOs WDK 多功能设备
- 物理设备对象 WDK 多功能设备
- PDOs WDK 多功能设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 463b22e614ac6e1243cd7781391a540694eec3a3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836799"
---
# <a name="supporting-multifunction-pci-devices"></a>支持多功能 PCI 设备





如果多功能 PCI 设备完全符合 PCI 多功能标准，PCI 总线驱动程序会枚举各个函数。 PCI 总线驱动程序管理在单个设备位置上存在多个函数的情况。 对于系统的其余部分，各个函数的运行方式类似于独立设备。

基于 NT 的平台上 PCI 多功能设备的供应商必须执行以下操作：

-   确保设备符合 PCI 多功能规范。

-   为设备的每个功能提供 PnP 函数驱动程序。

    由于系统提供的总线驱动程序处理多功能语义，因此函数驱动程序可以是在将函数打包为单个设备时使用的相同驱动程序。

-   为设备的每个功能提供一个 INF 文件。

    如果将这些文件打包为单独的设备，则 INF 文件可以是使用的相同文件。 INF 文件不需要任何特殊的多功能语义。

例如，下图显示了可能为带有 ISDN 和调制解调器功能的多功能 PCI 设备创建的示例设备堆栈。

![说明其父枚举每个函数的多功能设备的设备堆栈的关系图](images/mf-indep.png)

如上图所示，PCI 驱动程序会枚举两个子设备，而不是枚举一个多功能设备。 PnP 管理器会将每个子设备（如典型设备）、查找 INF 文件、加载相应的驱动程序、调用其 AddDevice 例程等进行处理，直到为每个设备创建了一个设备堆栈。 PCI 驱动程序仲裁子设备的资源，并管理设备的任何其他多功能。 多功能卡的供应商为 ISDN 和调制解调器设备提供了函数驱动程序和 Inf，就像它们是单独的设备一样。

该图重点介绍了每个函数的函数驱动程序和总线驱动程序及其关联的 FDO 和 PDO。 为了简单起见，将省略任何筛选器驱动程序 (和筛选器 DOs) 。

 

 




