---
title: 处理电源 IRP
description: 处理电源 IRP
ms.assetid: 0fe4f27a-101d-41af-8f00-fb36da5dc793
keywords:
- 电源管理 WDK 内核 Irp
- Irp WDK 电源管理
- 有关 power Irp power Irp WDK 内核
- IRP_MJ_POWER
- IRP_MN_QUERY_POWER
- IRP_MN_SET_POWER
- IRP_MN_WAIT_WAKE
- IRP_MN_POWER_SEQUENCE
- 电源状态 WDK 内核
- 指出 WDK 电源管理
- 更改电源状态 WDK 内核
- 节省电源 WDK 内核
- 睡眠电源管理 WDK 内核
- 查询能耗状态
- 睡眠状态的设备 WDK 电源管理
- I/O 请求数据包 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7896440bed422e3348c252e0f8c4d9e5809b45c5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371905"
---
# <a name="handling-power-irps"></a>处理电源 IRP





驱动程序处理中的电源 Irp [ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。 所有电源管理都请求具有重大的 IRP 代码[ **IRP\_MJ\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)和次要的以下代码之一：

[**IRP\_MN\_查询\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power) — 查询以确定是否更改电源状态为可行

[**IRP\_MN\_设置\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) — 从一个电源状态到另一个请求更改

[**IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake) — 请求启用设备唤醒本身或系统

[**IRP\_MN\_电源\_序列**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-power-sequence) — 请求以优化电源还原到特定设备的信息

为支持**IRP\_MN\_设置\_POWER**并**IRP\_MN\_查询\_POWER**是必需的。 所有驱动程序必须准备好处理这些 Irp。

为支持**IRP\_MN\_等待\_唤醒**是所必需的任何设备都可以被唤醒以响应外部信号的设备堆栈中的所有驱动程序。 驱动程序将发送此 IRP，以允许唤醒设备。

为支持**IRP\_MN\_POWER\_序列**是可选的。 此 IRP 为提供了优化需要较长的时间来恢复电源的设备。

系统电源操作或设备电源操作，可以指定 power IRP。 [系统电源 Irp](power-irps-for-the-system.md)并[Irp 用于单个设备的电源](power-irps-for-individual-devices.md)需要通过设备堆栈略有不同的路径，如以下各节中所述。

 

 




