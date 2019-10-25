---
title: DeviceWake
description: DeviceWake
ms.assetid: 3b82c095-1ee7-41e9-991e-ac0bcf959024
keywords:
- DeviceWake
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68f6aec1b46d96c20635ea2a384fc38a9e90b921
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828321"
---
# <a name="devicewake"></a>DeviceWake





[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)的**DeviceWake**成员包含设备可用于向唤醒事件发出信号的最小（最少驱动）设备电源状态，或**PowerDeviceUnspecified** （如果设备无法唤醒来响应外部信号。

总线驱动程序将设置此值。 较高级别的驱动程序可以将此值更改为更高的供电状态。 例如，如果总线驱动程序将**DeviceWake**设置为 D3，而设备堆栈进一步的驱动程序只支持从 D2 唤醒，则更高级别的驱动程序可以将值更改为 d2。

请注意，如果驱动程序更改**DeviceWake**，则可能还需要更改[**SystemWake**](systemwake.md) ，以避免与**DeviceState**数组中的系统到设备映射发生冲突。 例如，假定总线驱动程序设置以下各项：

-   **DeviceState**\[**PowerSystemSleeping1**\] = **PowerDeviceD1**

-   **DeviceState**\[**PowerSystemSleeping2**\] = **PowerDeviceD3**

-   **DeviceWake** = **PowerDeviceD3**

-   **SystemWake** = **PowerSystemSleeping2**

如果较高级别的驱动程序确定其设备无法从 D3 唤醒系统，但只能从 D2 或更高版本将**DeviceWake**更改为 d2。 但是，这种更改会导致不可能从 S2 到 D3 的映射。 请记住， **DeviceState**数组列出了设备在给定系统电源状态中可以支持的最高设备电源状态。 如果该示例中的系统电源状态为**PowerSystemSleeping2**，则无法**PowerDeviceD2**设备电源状态。 若要消除此问题，驱动程序还必须将**SystemWake**更改为**PowerSystemSleeping1**。 对于 **WakeFromD * * * x*和 **设备 * * x*设置也是如此。 驱动程序必须确保对**SystemWake**或**DeviceWake**所做的任何更改不会与 **WakeFromD * * * x*和 **设备 * * x*值冲突。 *WakeFromDx*和 **设备 * ** * 的值反映了驱动程序无法更改的硬件特征。

如果**SystemWake**和**DeviceWake**成员均为非零（即，不是**PowerSystemUnspecified**），则设备及其驱动程序在此系统上支持唤醒。

在非 ACPI 硬件上， **DeviceWake**成员包含零（**PowerSystemUnspecified**）。

 

 




