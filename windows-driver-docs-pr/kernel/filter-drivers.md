---
title: 筛选器驱动程序
description: 筛选器驱动程序
ms.assetid: 4def5503-bb0e-4bae-b048-4c8d25d62020
keywords:
- 筛选器驱动程序 WDK WDM
- 总线筛选器驱动程序 WDK WDM
- 较低级别筛选器驱动程序 WDK WDM
- 较高级别筛选器驱动程序 WDK WDM
- WDM 筛选器驱动程序 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48420bd2d318ba44cd45451329000c9f826d1ac8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359957"
---
# <a name="filter-drivers"></a>筛选器驱动程序





筛选器驱动程序被添加到值或修改设备的行为的可选驱动程序。 筛选器驱动程序可以服务一个或多个设备。

### <a href="" id="ddk-bus-filter-drivers-kg"></a>总线筛选器驱动程序

*总线筛选器驱动程序*通常将值添加到总线，并由 Microsoft 或系统 OEM 提供 (请参阅[可能驱动程序层](types-of-wdm-drivers.md#possible-driver-layers)图)。 总线筛选器驱动程序是可选的。 可以有任意数量的总线筛选器驱动程序。

总线筛选器驱动程序，例如，实现标准总线硬件的专有增强功能。

对于由 ACPI BIOS 中所述的设备，电源管理器将插入 Microsoft 提供*ACPI 筛选器*（总线筛选器驱动程序） 以上每个此类设备的总线驱动程序。 ACPI 筛选器执行设备的电源策略和为打开和关闭设备提供支持。 ACPI 筛选器对其他驱动程序是透明的并且不存在非 ACPI 的计算机上。

### <a href="" id="ddk-lower-level-filter-drivers-kg"></a>较低级别筛选器驱动程序

*较低级别筛选器驱动程序*通常会修改设备硬件的行为 (请参阅[可能驱动程序层](types-of-wdm-drivers.md#possible-driver-layers)图)。 它们通常由 Ihv 提供的都是可选的。 可以有任意数量的较低级别筛选器驱动程序的设备。

较低级别*设备*筛选器驱动程序监视和/或修改对特定设备的 I/O 请求。 通常情况下，此类筛选器重新定义以匹配预期的规范的硬件行为。

较低级别*类*筛选器驱动程序监视和/或修改某类设备的 I/O 请求。 例如，鼠标设备的较低级别类筛选器驱动程序可以提供加速，执行鼠标移动数据的非线性转换。

### <a href="" id="ddk-upper-level-filter-drivers-kg"></a>较高级别筛选器驱动程序

*较高级别筛选器驱动程序*通常为设备提供添加值功能 (请参阅[可能驱动程序层](types-of-wdm-drivers.md#possible-driver-layers)图)。 此类驱动程序通常由 Ihv 提供和都是可选的。 可以有任意数量的较高级别筛选器驱动程序的设备。

高级别的*设备*筛选器驱动程序添加特定设备值。 例如，键盘的较高级别设备筛选器驱动程序无法强制执行额外的安全检查。

高级别的*类*筛选器驱动程序添加特定类的所有设备的值。

 

 




