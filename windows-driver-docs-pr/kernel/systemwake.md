---
title: SystemWake
description: SystemWake
ms.assetid: 77390637-bb92-4634-a407-9a409a8a8acd
keywords:
- SystemWake
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72c5f9af3d512d091bd40e475467d41adf17ea9c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836125"
---
# <a name="systemwake"></a>SystemWake





[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)的**SystemWake**成员包含设备可从中唤醒系统的最低（最小）系统电源状态，如果设备无法唤醒系统，则为**PowerSystemUnspecified** 。

总线驱动程序在枚举设备时设置此值。 较高级别的驱动程序可以将此值更改为更高的状态，但不能将其更改为较低的电源状态。 例如，如果总线驱动程序将**SystemWake**设置为 S3，而设备堆栈进一步的驱动程序只支持从 S2 进行唤醒，则更高级别的驱动程序可以将该值更改为 s2。 如果驱动程序更改**SystemWake**，则可能还需要更改[**DeviceWake**](devicewake.md)，如下一节中所述。

驱动程序很少需要将更改后的值传播到设备堆栈中。 由于更改使得设备功能更具限制性，因此，较低的驱动程序不会看到它们无法处理的请求。 在前面的示例中，较高级别的驱动程序将无法从低于 S2 的更低的状态唤醒系统，因此，较低的驱动程序永远不会看到此类请求。 但是，如果驱动程序的驱动程序必须知道发生了任何更改，则在处理[**irp\_MN\_START\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)的过程中，它可以向其自己的设备堆栈发送 PnP [**IRP\_MN\_查询\_功能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)。

如果**SystemWake**和**DeviceWake**成员均为非零（即，不是**PowerSystemUnspecified**），则设备及其驱动程序在此系统上支持唤醒。

在非 ACPI 硬件上，此成员始终包含零（**PowerSystemUnspecified**）。

 

 




