---
title: 处理电源 IRP
description: 处理电源 IRP
ms.assetid: 0fe4f27a-101d-41af-8f00-fb36da5dc793
keywords:
- 电源管理 WDK 内核，Irp
- Irp WDK 电源管理
- power irp WDK 内核，关于 power Irp
- IRP_MJ_POWER
- IRP_MN_QUERY_POWER
- IRP_MN_SET_POWER
- IRP_MN_WAIT_WAKE
- IRP_MN_POWER_SEQUENCE
- 电源状态 WDK 内核
- 状态 WDK 电源管理
- 更改电源状态 WDK 内核
- 保存电源 WDK 内核
- 睡眠电源管理 WDK 内核
- 查询电源状态
- 睡眠设备 WDK 电源管理
- I/o 请求数据包 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec6ae561af2a1a93c1c0c8a1d1b2700f1a8f4de1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836488"
---
# <a name="handling-power-irps"></a>处理电源 IRP





驱动程序在[*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程中处理电源 irp。 所有电源管理请求都具有主要 IRP 代码[**irp\_MJ\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)和以下次要代码之一：

[**IRP\_MN\_QUERY\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power) -查询以确定更改电源状态是否可行

[**IRP\_MN\_设置\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) -请求从一种电源状态更改为另一种电源状态

[**IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake) -请求启用设备来唤醒自身或系统

[**IRP\_MN\_电源\_序列**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-power-sequence) -请求信息以优化到特定设备的电源恢复

支持**IRP\_MN\_设置\_POWER** and **IRP\_MN\_查询**\_需要满足此要求。 所有驱动程序必须准备好处理这些 Irp。

支持**IRP\_MN\_等待**任何设备的设备堆栈中的所有驱动程序\_唤醒，任何设备都可以唤醒响应外部信号。 驱动程序将发送此 IRP，使设备能够进行唤醒。

支持**IRP\_MN\_POWER\_序列**是可选的。 此 IRP 为需要很长时间才能恢复电源的设备提供优化。

Power IRP 可以指定系统电源操作或设备电源操作。 适用于单个设备的系统和[电源 irp](power-irps-for-individual-devices.md)的[power irp](power-irps-for-the-system.md)通过设备堆栈获取略微不同的路径，如以下各节中所述。

 

 




