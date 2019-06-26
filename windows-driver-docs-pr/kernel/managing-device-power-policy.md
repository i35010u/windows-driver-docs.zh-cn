---
title: 管理设备电源策略
description: 管理设备电源策略
ms.assetid: f6f9ab40-4d51-4181-ac11-ff7af42370af
keywords:
- 设备电源策略 WDK 内核
- 电源策略 WDK 内核
- 设备电源策略所有者 WDK 内核
- 功能的驱动程序 WDK 电源管理
- 设备电源状态 WDK 内核
- 初始设备电源状态 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0060c021eca15cd072934e4f3a0236348b1f806
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365795"
---
# <a name="managing-device-power-policy"></a>管理设备电源策略





正如电源管理器维护和管理系统的电源策略，每个设备的设备堆栈中的一个驱动程序维护和管理设备的电源策略。 此驱动程序*设备电源策略所有者*设备。

设备电源策略所有者是驱动程序有关的设备使用情况和电源状态信息具有充分的信息。 它不以物理方式需要能够设置电源设备的设备寄存器，打开和关闭，但它必须能够确定当设备正在使用中、 处于空闲状态，以及它应更改电源状态，当。

通常情况下，设备功能驱动程序是其电源策略所有者，尽管对于某些设备另一个驱动程序或系统组件可能认为此角色。 有关类型的驱动程序涉及中电源管理的详细信息，请参阅[WDM 驱动程序类型](types-of-wdm-drivers.md)。

某些驱动程序充当 （创建 FDO） 的一台设备的功能驱动程序和总线驱动程序 （创建 PDO） 枚举的子设备。 在其强大的功能和 PnP Irp 的调度例程，这样的驱动程序必须将其处理 Irp 发送到 FDO 和那些发送到 PDO 区分开来。

例如，SCSI 适配器的驱动程序可能执行的角色功能驱动程序 （创建 FDO） 适配器本身和总线驱动程序 （创建 PDO） 连接到的适配器的磁盘。 在其容量中作为函数驱动程序/策略所有者的 SCSI 适配器，此驱动程序接收 Irp 系统，并请求该 SCSI 适配器的设备 Irp。 在其容量中作为总线驱动程序的磁盘，它将处理并完成设备 Irp 指定磁盘 PDOs 它创建的。 只是因为该驱动程序拥有一台设备 (FDO) 的电源策略并不意味着它拥有子设备 (PDO) 的电源策略。

设备电源策略所有者负责以下：

-   通过调用将在设备的初始电源状态设置为 D0 [ **PoSetPowerState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-posetpowerstate)的方式与处理插 manager [ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求。

    设备应打开电源，根据需要;例如，设备必须启动以句柄的 I/O 请求。 设备电源策略所有者负责确定何时需要其设备，确保设备电源已打开，并设置正确的设备电源状态。 典型的设备的即插即用的启动设备 IRP 已经完成的时间应开机。

    作为一般规则，大多数设备应关机时在不使用，即使系统处于工作状态。

-   通过调用以响应系统电源请求发送设备电源请求[ **PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp)。

    例如，当策略所有者收到系统集 power IRP，它将发送设备集 power IRP。 当系统进入任何睡眠状态时，大多数设备输入 D3。 **DeviceState**数组[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)结构列出了设备可以维护的每个系统电源的 highest-powered 状态状态。 (请参阅[报告设备电源功能](reporting-device-power-capabilities.md)。)

-   检测当设备处于空闲状态并使其进入睡眠状态以节约能源。

    电源管理器或设备的策略所有者可以检测空闲设备并发送设备电源 IRP 以更改其状态。 有关详细信息，请参阅[检测空闲的设备](detecting-an-idle-device.md)。

-   返回到工作状态时所需其设备。

    当 I/O 请求到达时处于睡眠状态的设备时，设备的驱动程序应返回到工作状态。

-   启用和禁用唤醒时请求其设备。

    设备的电源策略所有者发送并取消等待/唤醒 Irp，如中所述[支持设备的已唤醒功能](supporting-devices-that-have-wake-up-capabilities.md)。

 

 




