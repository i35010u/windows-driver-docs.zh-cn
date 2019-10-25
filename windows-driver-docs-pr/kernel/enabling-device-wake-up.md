---
title: 启用设备唤醒
description: 启用设备唤醒
ms.assetid: 1c3b9ebc-cc77-4562-9c57-56f2c9a69772
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
ms.openlocfilehash: b8a4e488c13fc3705d9b83cc8fa98e31714648fa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836788"
---
# <a name="enabling-device-wake-up"></a>启用设备唤醒





如果设备支持唤醒，则其电源策略所有者必须能够启用和禁用设备唤醒。 驱动程序通过将[**irp\_MJ 发送\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)具有次要函数代码 IRP 的 POWER REQUEST [ **\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)并禁用唤醒，方法是通过取消以前发送的**IRP\_MN\_等待\_唤醒**。 一台设备只能有一个**IRP\_MN\_等待\_唤醒**请求一次挂起。

若要确定设备是否支持唤醒、设备电源状态（它可以通过这些状态进行唤醒，以及设备可以从其唤醒系统的系统电源状态），驱动程序将检查**SystemWake**、 **DeviceWake**和 **WakeFromD * * ** 设备中的 x 成员[ **\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)结构。

有关在驱动程序中启用、禁用和响应唤醒信号的详细信息，请参阅[支持具有唤醒功能的设备](supporting-devices-that-have-wake-up-capabilities.md)。

 

 




