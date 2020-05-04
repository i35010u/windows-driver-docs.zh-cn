---
title: 筛选器驱动程序
description: 筛选器驱动程序
ms.assetid: 4def5503-bb0e-4bae-b048-4c8d25d62020
keywords:
- 筛选器驱动程序 WDK WDM
- 总线筛选器驱动程序 WDK WDM
- 下层筛选器驱动程序 WDK WDM
- 上层筛选器驱动程序 WDK WDM
- WDM 筛选器驱动程序 WDK
ms.date: 06/16/2017
ms.localizationpriority: High
ms.openlocfilehash: c0791a48f94db8a9be106498a32917fe6f0f7c96
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "72007648"
---
# <a name="filter-drivers"></a>筛选器驱动程序





筛选器驱动程序是可选驱动程序，可为设备提供增值功能或修改设备的行为。 筛选器驱动程序可以为一个或多个设备服务。

### <a name="bus-filter-drivers"></a><a href="" id="ddk-bus-filter-drivers-kg"></a>总线筛选器驱动程序

 总线筛选器驱动程序通常为总线提供增值功能，由 Microsoft 或系统 OEM 提供（请参见[可能的驱动程序层](types-of-wdm-drivers.md#possible-driver-layers)图）。 总线筛选器驱动程序是可选的。 一个总线可以有任意数量的总线筛选器驱动程序。

例如，总线筛选器驱动程序可以对标准总线硬件实现专有增强功能。

对于 ACPI BIOS 描述的设备，电源管理器会将 Microsoft 提供的 ACPI 筛选器  （总线筛选器驱动程序）插入到每个此类设备的总线驱动程序之上。 ACPI 筛选器执行设备电源策略，并打开和关闭设备。 ACPI 筛选器对其他驱动程序是透明的，且在非 ACPI 计算机上不存在。

### <a name="lower-level-filter-drivers"></a><a href="" id="ddk-lower-level-filter-drivers-kg"></a>下层筛选器驱动程序

*下层筛选器驱动程序*通常会修改设备硬件的行为（请参见[可能的驱动程序层](types-of-wdm-drivers.md#possible-driver-layers)图）。 它们是可选的，通常由 IHV 提供。 一个设备可以有任意数量的底层筛选器驱动程序。

下层设备  筛选器驱动程序监视和/或修改特定设备的 I/O 请求。 通常，此类筛选器会重新定义硬件行为，以使其符合预期规范。

下层类  筛选器驱动程序监视和/或修改一类设备的 I/O 请求。 例如，用于鼠标设备的下层类筛选器驱动程序可以提供加速，执行鼠标移动数据的非线性转换。

### <a name="upper-level-filter-drivers"></a><a href="" id="ddk-upper-level-filter-drivers-kg"></a>上层筛选器驱动程序

上层筛选器驱动程序  通常为设备提供增值功能（请参见[可能的驱动程序层](types-of-wdm-drivers.md#possible-driver-layers)图）。 此类驱动程序是可选的，通常由 IHV 提供。 一个设备可以有任意数量的上层筛选器驱动程序。

上层设备  筛选器驱动程序可以为特定设备提供增值功能。 例如，键盘的上层设备筛选器驱动程序可能会强制执行其他安全检查。

上层类  筛选器驱动程序为特定类的所有设备提供增值功能。

 

 




