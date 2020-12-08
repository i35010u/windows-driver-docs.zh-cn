---
title: 管理设备电源策略
description: 管理设备电源策略
keywords:
- 设备电源策略 WDK 内核
- 电源策略 WDK 内核
- 设备电源策略所有者 WDK 内核
- 函数驱动程序 WDK 电源管理
- 设备电源状态 WDK 内核
- 初始设备电源状态 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d9038b8d19eec2750ebdece6c55d4bc5c274bb4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825119"
---
# <a name="managing-device-power-policy"></a>管理设备电源策略





就像 power manager 维护和管理系统的电源策略一样，每台设备的设备堆栈中的一个驱动程序都维护并管理设备的电源策略。 此驱动程序是设备的 *设备电源策略所有者* 。

设备电源策略所有者是包含有关设备使用情况和电源状态的最多信息的驱动程序。 它不需要实际将设备寄存器设置为打开和关闭设备，但它必须能够确定设备的使用时间、空闲时间以及何时应更改电源状态。

通常，设备的函数驱动程序是其电源策略所有者，但对于某些设备，其他驱动程序或系统组件可能会担任此角色。 有关电源管理中涉及的驱动程序类型的详细信息，请参阅 [WDM 驱动程序的类型](types-of-wdm-drivers.md)。

某些驱动程序充当一台设备的函数驱动程序， (创建 FDO) 和总线驱动程序 (为枚举的子设备创建 PDO) 。 对于电源和 PnP Irp，此类驱动程序必须区分发送到 FDO 的 Irp 处理和发送到 PDO 的 Irp。

例如，SCSI 适配器的驱动程序可能会执行功能驱动程序的角色 (为适配器本身和总线驱动程序创建 FDO) ， (为附加到适配器的磁盘创建 PDO) 。 该驱动程序在其容量上作为 SCSI 适配器的函数驱动程序/策略所有者，接收系统 Irp，并请求 SCSI 适配器的设备 Irp。 作为磁盘的总线驱动程序，它将处理和完成指定其创建的磁盘 PDOs 的设备 Irp。 仅由于驱动程序拥有一个设备的电源策略 (FDO) 并不意味着它拥有 (PDO) 的子设备的电源策略。

设备电源策略所有者负责以下操作：

-   在处理即插即用 manager 的 [**IRP \_ MN \_ START \_ 设备**](./irp-mn-start-device.md)请求时，通过调用 [**PoSetPowerState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)将设备的初始电源状态设置为 D0。

    设备应根据需要接通电源;例如，设备必须开机才能处理 i/o 请求。 设备电源策略所有者负责确定何时需要其设备、确保设备电源已打开并设置正确的设备电源状态。 在 PnP 启动设备 IRP 完成后，典型设备应该开机。

    作为一般规则，大多数设备应该在不使用时关闭，即使系统处于工作状态也是如此。

-   通过调用 [**PoRequestPowerIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)发送设备电源请求以响应系统电源请求。

    例如，当策略所有者接收到系统集-电源 IRP 时，它将发送一个设备设置-电源 IRP。 大多数设备进入 D3 时，系统进入任何休眠状态。 [**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构中的 **DeviceState** 数组列出设备可以为每个系统电源状态维护的最高的状态。  (参阅 [报告设备电源功能](reporting-device-power-capabilities.md)。 ) 

-   检测设备处于空闲状态的时间，并将其置于睡眠状态以节省能源。

    电源管理器或设备策略所有者可以检测空闲设备，并发送设备电源 IRP 来更改其状态。 有关详细信息，请参阅 [检测空闲设备](detecting-an-idle-device.md)。

-   需要时将其设备返回到工作状态。

    当 i/o 请求到达睡眠设备时，设备的驱动程序应将其返回到工作状态。

-   请求时启用和禁用其设备唤醒。

    设备电源策略所有者发送和取消等待/唤醒 Irp，如 [支持具有 Wake-Up 功能的设备](supporting-devices-that-have-wake-up-capabilities.md)中所述。

 

