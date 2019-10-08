---
title: 筛选器驱动程序
description: 筛选器驱动程序
ms.assetid: 4def5503-bb0e-4bae-b048-4c8d25d62020
keywords:
- 筛选器驱动程序 WDK WDM
- 总线筛选器驱动程序 WDK WDM
- 底层筛选器驱动程序 WDK WDM
- 高级筛选器驱动程序 WDK WDM
- WDM 筛选器驱动程序 WDK
ms.date: 06/16/2017
ms.localizationpriority: High
ms.openlocfilehash: c0791a48f94db8a9be106498a32917fe6f0f7c96
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007648"
---
# <a name="filter-drivers"></a>筛选器驱动程序





筛选器驱动程序是可选的驱动程序，可添加值或修改设备的行为。 筛选器驱动程序可以为一个或多个设备服务。

### <a href="" id="ddk-bus-filter-drivers-kg"></a>总线筛选器驱动程序

*总线筛选器驱动程序*通常将值添加到总线，由 Microsoft 或系统 OEM 提供（请参阅[可能的驱动程序层](types-of-wdm-drivers.md#possible-driver-layers)图）。 总线筛选器驱动程序是可选的。 总线可以有任意数量的总线筛选器驱动程序。

例如，总线筛选器驱动程序可以对标准总线硬件实施专有增强功能。

对于 ACPI BIOS 描述的设备，电源管理器会将 Microsoft 提供的*ACPI 筛选器*（总线筛选器驱动程序）插入到每个此类设备的总线驱动程序之上。 ACPI 筛选器执行设备电源策略，并打开和关闭设备。 ACPI 筛选器对其他驱动程序是透明的，不存在于非 ACPI 计算机上。

### <a href="" id="ddk-lower-level-filter-drivers-kg"></a>低级筛选器驱动程序

*较低级别的筛选器驱动程序*通常会修改设备硬件的行为（请参阅[可能的驱动程序层](types-of-wdm-drivers.md#possible-driver-layers)图）。 它们通常由 Ihv 提供，并且是可选的。 一个设备可以有任意数量的低级筛选器驱动程序。

较低级别的*设备*筛选器驱动程序监视和/或修改特定设备的 i/o 请求。 通常，此类筛选器会将硬件行为重新定义为符合预期规范。

较低级别的*类*筛选器驱动程序监视和/或修改一类设备的 i/o 请求。 例如，用于鼠标设备的较低级别类筛选器驱动程序可以提供加速，执行鼠标移动数据的非线性转换。

### <a href="" id="ddk-upper-level-filter-drivers-kg"></a>高级筛选器驱动程序

*上层筛选器驱动程序*通常为设备提供附加的值功能（请参阅[可能的驱动程序层](types-of-wdm-drivers.md#possible-driver-layers)图）。 此类驱动程序通常由 Ihv 提供，并且是可选的。 一个设备可以有任意数量的高级筛选器驱动程序。

上层*设备*筛选器驱动程序为特定设备添加值。 例如，键盘的高级设备筛选器驱动程序可能会强制执行其他安全检查。

高级*类*筛选器驱动程序为特定类的所有设备添加值。

 

 




