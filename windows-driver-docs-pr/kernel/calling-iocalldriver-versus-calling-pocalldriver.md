---
title: 调用 IoCallDriver 与调用 PoCallDriver
description: 调用 IoCallDriver 与调用 PoCallDriver
ms.assetid: a47e2310-e89b-4552-bbe3-d4984ae8b564
keywords:
- PoCallDriver
- 活动电源 Irp WDK 内核
- power Irp WDK 内核，IoCallDriver 与 PoCallDriver
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: da58916b9756dbe2ec53a8e8b5ea215c53527a96
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190258"
---
# <a name="calling-iocalldriver-versus-calling-pocalldriver"></a>调用 IoCallDriver 与调用 PoCallDriver





从 Windows Vista 开始，驱动程序应调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 而不是 [**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)，将电源 irp 传递到下一个较低版本的驱动程序。 在 Windows Server 2003、Windows XP 和 Windows 2000 中，驱动程序必须调用 **PoCallDriver**（而不是 **IoCallDriver**），才能将电源 irp 传递到下一个较低版本的驱动程序。 但请注意，使用相同代码的驱动程序在 Windows Vista 和更早版本的 Windows 版本中运行时，必须调用 **PoCallDriver**，而不是 **IoCallDriver**。

从 Windows Vista 开始， [**PoRequestPowerIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp) 和 **IoCallDriver** 确保电源管理器在整个系统中正确同步 power irp。 在 Windows Server 2003、Windows XP 和 Windows 2000、 **PoRequestPowerIrp**、 **PoCallDriver**和 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)中，确保电源管理器在整个系统中正确同步 power irp。

系统将限制活动电源 Irp 的数目，如下所示：

-   在任何给定时间，都不能有多个系统电源 IRP (**IRP \_ MN \_ 设置 \_ 电源**) 。

-   不能有多个设备设置-power IRP ** (\_ IRP \_ MN \_) 设置 ** 每个 PDO 在给定时间都可以为每个 PDO 激活。

-   在任何给定时间，都不能有多个设备电源 IRP 需要电涌才能在系统中的任意位置处于活动状态。

为了确保两个浪涌设备不会尝试同时通电，电源管理器会跟踪整个系统中的活动浪涌电源 Irp，并允许一次只有一个处于活动状态。 在活动的浪涌 IRP 完成之前，无法启动其他浪涌 IRP。

由于对浪涌 Irp 的这些限制，在其他设备的浪涌 IRP 完成时，设备电源 IRP 可能会阻塞。 在调试过程中，驱动程序编写人员应注意到此行为。

 

