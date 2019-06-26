---
title: 打开设备的电源
description: 打开设备的电源
ms.assetid: 115cc904-922d-447e-b221-cb3e489dd08d
keywords:
- I/O WDK 电源管理
- 设备电源 ups WDK 内核
- 启动设备 WDK 内核增强
- IRP_MN_SET_POWER
- 工作状态返回 WDK 电源管理
- 开启设备 WDK 电源管理
- 自动电源 ups WDK 内核
- 在 power WDK 内核
- Irp WDK 电源管理
- 启动 power management WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47030c7259405113ce53cfca4d11eae43107d268
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374169"
---
# <a name="powering-up-a-device"></a>打开设备的电源





当总线驱动程序处理 PnP [ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)请求一个其子设备，它会启动设备并调用[**PoSetPowerState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-posetpowerstate)向电源管理器中报告设备电源状态。 打开设备是设备启动一个隐式部分。 设备电源策略所有者不会发送[ **IRP\_MN\_设置\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)为请求**PowerDeviceD0**，因此驱动程序应该不会收到这些 Irp 在启动时。

当设备电源以节省电能时，其驱动程序应接通电源的 I/O 请求到达时。 在这种情况下，必须将发送设备电源策略所有者**IRP\_MN\_设置\_POWER**若要将设备恢复为工作状态。 IRP 完成后，设备的驱动程序停止队列 I/O 并开始处理队列的请求。

 

 




