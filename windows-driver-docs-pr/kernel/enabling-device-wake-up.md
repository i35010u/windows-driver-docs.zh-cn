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
- 还原 power WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b48d4dfe950e7909bff5ec52ed259f3027241325
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384948"
---
# <a name="enabling-device-wake-up"></a>启用设备唤醒





如果设备支持唤醒，其电源策略所有者必须能够启用和禁用唤醒设备。 驱动程序，会通过将发送的唤醒[ **IRP\_MJ\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)次要功能代码请求[ **IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake) ，并禁用通过取消先前发送的唤醒**IRP\_MN\_等待\_唤醒**。 设备只能有一个**IRP\_MN\_等待\_唤醒**一次请求挂起。

若要确定是否在其设备支持唤醒，设备电源状态从它可以发出信号唤醒，并从该设备可以唤醒系统的系统电源状态，驱动程序将检查**SystemWake**， **DeviceWake**，和 **WakeFromD * * * x*中的成员[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)结构。

有关启用的详细信息，禁用和响应唤醒信号中驱动程序，请参阅[支持设备的已唤醒功能](supporting-devices-that-have-wake-up-capabilities.md)。

 

 




