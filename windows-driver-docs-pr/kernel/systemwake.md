---
title: SystemWake
description: SystemWake
ms.assetid: 77390637-bb92-4634-a407-9a409a8a8acd
keywords:
- SystemWake
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc0dd08b7d799465daaaa88f24f415b7e89b7c6d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382964"
---
# <a name="systemwake"></a>SystemWake





**SystemWake**的成员[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)包含设备可以将系统唤醒从其最低 （最少支持） 的系统电源状态或**PowerSystemUnspecified**如果设备不能将系统唤醒。

当枚举设备时，总线驱动程序设置此值。 更高级别的驱动程序可以将值更改为 higher-powered 状态，但不能将其更改为低功率状态。 例如，如果总线驱动程序设置**SystemWake**到 S3，但驱动程序进一步启动设备堆栈支持唤醒只能从 S2，更高级别的驱动程序可以将值更改为 S2。 如果驱动程序更改**SystemWake**，它可能还需要更改[ **DeviceWake**](devicewake.md)、 下一节中所述。

驱动程序很少需要传播已更改的值，再减少设备堆栈。 因为更改使设备功能的更多限制，较低的驱动程序不会看到它们不能处理的请求。 在上一示例中，更高级别的驱动程序将失败来唤醒从 S2，比低功率状态系统，因此较低的驱动程序永远不会看到此类请求的任何请求。 但是，如果较低的驱动程序必须了解的任何更改，它可以发送 PnP [ **IRP\_MN\_查询\_功能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)到其自己的其处理过程中的设备堆栈[ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)。

如果这两个**SystemWake**并**DeviceWake**成员均不为零 (即，不**PowerSystemUnspecified**)，然后设备和其驱动程序支持唤醒此系统上。

在非 ACPI 硬件上，此成员始终包含零 (**PowerSystemUnspecified**)。

 

 




