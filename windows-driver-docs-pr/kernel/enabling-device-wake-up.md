---
title: 启用设备唤醒
description: 启用设备唤醒
keywords:
- Irp WDK 电源管理
- 唤醒设备
- 唤醒功能 WDK 电源管理
- 设备唤醒 ups WDK 电源管理
- IRP_MN_WAIT_WAKE
- IRP_MJ_POWER
- DEVICE_CAPABILITIES 结构
- 正在还原电源 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b040ee5a7523272d99261ffcedb1ace67db0ecff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820671"
---
# <a name="enabling-device-wake-up"></a>启用设备唤醒





如果设备支持唤醒，则其电源策略所有者必须能够启用和禁用设备唤醒。 驱动程序通过向次要函数代码 [**IRP \_ MN \_ 等待 \_ 唤醒**](./irp-mn-wait-wake.md)发送 [**irp \_ MJ \_ 电源**](./irp-mj-power.md)请求来唤醒，并通过取消以前发送的 **IRP \_ MN \_ 等待 \_ 唤醒** 来禁用唤醒。 一次设备只能有一个 **IRP \_ MN \_ 等待 \_ 唤醒** 请求处于挂起状态。

若要确定设备是否支持唤醒、设备电源状态（它可以通过这些状态进行唤醒，以及设备可以从哪个系统供电状态唤醒系统），驱动程序将检查 [**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构中的 **SystemWake**、 **DeviceWake** 和 **WakeFromD**_x_ 成员。

有关在驱动程序中启用、禁用和响应唤醒信号的详细信息，请参阅 [支持具有 Wake-Up 功能的设备](supporting-devices-that-have-wake-up-capabilities.md)。

 

