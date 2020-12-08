---
title: DeviceWake
description: DeviceWake
keywords:
- DeviceWake
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce4b7acad3c8227eecf3060a0fba916aac4759ee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792769"
---
# <a name="devicewake"></a>DeviceWake





[**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)的 **DeviceWake** 成员包含设备可用于向唤醒事件发出信号的最小 () 设备电源状态，如果设备无法唤醒以响应外部信号，则为 **PowerDeviceUnspecified** 。

总线驱动程序将设置此值。 较高级别的驱动程序可以将此值更改为更高的供电状态。 例如，如果总线驱动程序将 **DeviceWake** 设置为 D3，而设备堆栈进一步的驱动程序只支持从 D2 唤醒，则更高级别的驱动程序可以将值更改为 d2。

请注意，如果驱动程序更改 **DeviceWake**，则可能还需要更改 [**SystemWake**](systemwake.md) ，以避免与 **DeviceState** 数组中的系统到设备映射发生冲突。 例如，假定总线驱动程序设置以下各项：

-   **DeviceState** \[**PowerSystemSleeping1** \] PowerSystemSleeping1  = **PowerDeviceD1**

-   **DeviceState** \[**PowerSystemSleeping2** \] PowerSystemSleeping2  = **PowerDeviceD3**

-   **DeviceWake**  = **PowerDeviceD3**

-   **SystemWake**  = **PowerSystemSleeping2**

如果较高级别的驱动程序确定其设备无法从 D3 唤醒系统，但只能从 D2 或更高版本将 **DeviceWake** 更改为 d2。 但是，这种更改会导致不可能从 S2 到 D3 的映射。 请记住， **DeviceState** 数组列出了设备在给定系统电源状态中可以支持的最高设备电源状态。 如果该示例中的系统电源状态为 **PowerSystemSleeping2**，则无法 **PowerDeviceD2** 设备电源状态。 若要消除此问题，驱动程序还必须将 **SystemWake** 更改为 **PowerSystemSleeping1**。 对于 **WakeFromD**_x_ 和 **设备**_x_ 设置也是如此。 驱动程序必须确保对 **SystemWake** 或 **DeviceWake** 所做的任何更改不会与 **WakeFromD**_x_ 和 **设备**_x_ 值冲突。 *WakeFromDx* 和 **设备**_x_ 的值反映了驱动程序无法更改的硬件特征。

如果 " **SystemWake** " 和 " **DeviceWake** " 成员均为非零 (即，而不是 **PowerSystemUnspecified**) ，则设备及其驱动程序在此系统上支持唤醒。

在非 ACPI 硬件上， **DeviceWake** 成员包含零 (**PowerSystemUnspecified**) 。

 

