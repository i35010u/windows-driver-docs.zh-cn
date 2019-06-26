---
title: DeviceWake
description: DeviceWake
ms.assetid: 3b82c095-1ee7-41e9-991e-ac0bcf959024
keywords:
- DeviceWake
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32e8d2f2a049a7503cc9c0832f72925168fe43e0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384996"
---
# <a name="devicewake"></a>DeviceWake





**DeviceWake**的成员[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)包含从其设备，可以发出唤醒最低 （最少的） 设备电源状态事件，或**PowerDeviceUnspecified**如果设备无法唤醒以响应外部信号。

总线驱动程序设置此值。 更高级别的驱动程序可以将值更改为 higher-powered 状态。 例如，如果总线驱动程序设置**DeviceWake** D3 但驱动程序进一步启动设备堆栈支持唤醒只能从 D2，更高级别的驱动程序可以将值更改为 D2。

请注意，如果驱动程序更改**DeviceWake**，它可能还需要更改[ **SystemWake** ](systemwake.md)以避免与中的系统设备映射冲突**DeviceState**数组。 例如，假定总线驱动程序设置如下：

-   **DeviceState**\[**PowerSystemSleeping1**\] = **PowerDeviceD1**

-   **DeviceState**\[**PowerSystemSleeping2**\] = **PowerDeviceD3**

-   **DeviceWake** = **PowerDeviceD3**

-   **SystemWake** = **PowerSystemSleeping2**

如果更高级别的驱动程序确定其设备不能从 D3，系统唤醒，但仅能从 D2 或更高版本，可以更改**DeviceWake**到 D2。 但是，此更改会导致映射，从 s2 切换到 D3 不可能。 请记住， **DeviceState**数组列出了设备可以支持为给定的系统电源状态的最高设备电源状态。 如果在示例中的系统电源状态为**PowerSystemSleeping2**，不能将设备电源状态**PowerDeviceD2**。 若要消除此问题，该驱动程序还必须更改**SystemWake**到**PowerSystemSleeping1**。 同样适用于 **WakeFromD * * * x*和 **DeviceD * * * x*设置。 驱动程序必须确保任何值发生为其更改为使**SystemWake**或**DeviceWake**与不冲突 **WakeFromD * * * x*和 **DeviceD * * * x*值。 值*WakeFromDx*和 **DeviceD * * * x*反映驱动程序不能更改的硬件特征。

如果这两个**SystemWake**并**DeviceWake**成员均不为零 (即，不**PowerSystemUnspecified**)，然后设备和其驱动程序支持唤醒此系统上。

在非 ACPI 硬件**DeviceWake**成员包含零 (**PowerSystemUnspecified**)。

 

 




