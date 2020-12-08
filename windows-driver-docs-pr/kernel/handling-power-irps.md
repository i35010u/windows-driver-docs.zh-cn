---
title: 处理电源 IRP
description: 处理电源 IRP
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
ms.openlocfilehash: 2243e65379cb146ec99b7fb4ae708970c9ba2fd1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830395"
---
# <a name="handling-power-irps"></a>处理电源 IRP





驱动程序在 [*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中处理电源 irp。 所有电源管理请求都具有主要 IRP 代码 [**irp \_ MJ \_**](./irp-mj-power.md) ，并具有以下次要代码之一：

[**IRP \_MN \_ QUERY \_ power**](./irp-mn-query-power.md) -用于确定更改电源状态是否可行的查询

[**IRP \_MN \_ 设置 \_ 电源**](./irp-mn-set-power.md) -请求从一个电源状态更改为另一个电源状态

[**IRP \_MN \_ 等待 \_ 唤醒**](./irp-mn-wait-wake.md) -请求启用设备以唤醒自身或系统

[**IRP \_MN \_ 幂 \_ 序列**](./irp-mn-power-sequence.md) -请求信息以优化到特定设备的电源恢复

需要对 **IRP \_ MN \_ SET \_ power** 和 **IRP \_ MN \_ 查询 \_ 能力** 进行支持。 所有驱动程序必须准备好处理这些 Irp。

对于可以唤醒以响应外部信号的任何设备，设备堆栈中的所有驱动程序都需要支持 **IRP \_ MN \_ 等待 \_ 唤醒** 。 驱动程序将发送此 IRP，使设备能够进行唤醒。

支持 **IRP \_ MN \_ 电源 \_ 序列** 是可选的。 此 IRP 为需要很长时间才能恢复电源的设备提供优化。

Power IRP 可以指定系统电源操作或设备电源操作。 适用于单个设备的系统和[电源 irp](power-irps-for-individual-devices.md)的[power irp](power-irps-for-the-system.md)通过设备堆栈获取略微不同的路径，如以下各节中所述。

 

