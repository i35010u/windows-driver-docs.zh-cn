---
title: SystemWake
description: SystemWake
ms.assetid: 77390637-bb92-4634-a407-9a409a8a8acd
keywords:
- SystemWake
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e3cdf4dbd5891b2f55ca65578ea3638b676f9b8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185915"
---
# <a name="systemwake"></a>SystemWake





[**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)的**SystemWake**成员包含最小 (的最小) 系统电源状态，在该状态下设备可以唤醒系统; 如果设备无法唤醒系统，则为**PowerSystemUnspecified** 。

总线驱动程序在枚举设备时设置此值。 较高级别的驱动程序可以将此值更改为更高的状态，但不能将其更改为较低的电源状态。 例如，如果总线驱动程序将 **SystemWake** 设置为 S3，而设备堆栈进一步的驱动程序只支持从 S2 进行唤醒，则更高级别的驱动程序可以将该值更改为 s2。 如果驱动程序更改 **SystemWake**，则可能还需要更改 [**DeviceWake**](devicewake.md)，如下一节中所述。

驱动程序很少需要将更改后的值传播到设备堆栈中。 由于更改使得设备功能更具限制性，因此，较低的驱动程序不会看到它们无法处理的请求。 在前面的示例中，较高级别的驱动程序将无法从低于 S2 的更低的状态唤醒系统，因此，较低的驱动程序永远不会看到此类请求。 但是，如果较低的驱动程序必须知道发生了任何更改，则在处理[**IRP \_ MN \_ 启动 \_ 设备**](./irp-mn-start-device.md)的过程中，它可以向其自己的设备堆栈发送 PnP [**IRP \_ MN \_ 查询 \_ 功能**](./irp-mn-query-capabilities.md)。

如果 " **SystemWake** " 和 " **DeviceWake** " 成员均为非零 (即，而不是 **PowerSystemUnspecified**) ，则设备及其驱动程序在此系统上支持唤醒。

在非 ACPI 硬件上，此成员始终包含零 (**PowerSystemUnspecified**) 。

 

