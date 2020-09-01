---
title: 驱动程序的电源管理责任
description: 驱动程序的电源管理责任
ms.assetid: c42a5b95-76f3-4975-b452-4858bbbe532e
keywords:
- 电源管理 WDK 内核，驱动程序职责
- 驱动程序电源责任 WDk 内核
- 保存电源 WDK 内核
- 电源管理 WDK 内核，电源状态
- 电源状态 WDK 内核
- 状态 WDK 电源管理
- 系统电源状态 WDK 内核，电源管理
- 设备电源状态 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45628a53230b61b6d639f88ae13c8f18bb897dba
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184427"
---
# <a name="power-management-responsibilities-for-drivers"></a>驱动程序的电源管理责任





支持电源管理的驱动程序负责：

在 PnP 枚举过程中[报告设备电源功能](reporting-device-power-capabilities.md)。

[设置电源管理的设备对象标志](setting-device-object-flags-for-power-management.md)。

处理电源管理器或驱动程序发送的[电源 irp](handling-power-irps.md) 。

在系统启动或空闲关闭后，尽快启动[设备](powering-up-a-device.md)。

在系统关闭时关闭设备，或在空闲时使[设备](powering-down-a-device.md)进入睡眠状态。

如果设备支持唤醒功能，则[启用设备唤醒](enabling-device-wake-up.md)。

如果设备支持降低性能或功能以降低功率消耗，则[管理设备性能状态](managing-device-performance-states.md)。

并非每个设备堆栈中的每个驱动程序都执行所有这些任务。 通常情况下，总线驱动程序会报告功能、设置标志并操作物理设备，设备电源策略管理器通常 (功能驱动程序) 发出请求以使设备进入睡眠状态并启用唤醒。

除了少数例外情况外，驱动程序会开机并关闭其设备，并使设备可以进行唤醒，以响应电源 Irp，也就是说，具有主要代码 [**IRP \_ MJ \_ 功能**](./irp-mj-power.md)的 irp。 电源管理器可以通过电源管理器发送电源 Irp，在某些情况下，可以由驱动程序发送。

 

