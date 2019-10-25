---
title: 打开设备的电源
description: 打开设备的电源
ms.assetid: 115cc904-922d-447e-b221-cb3e489dd08d
keywords:
- I/o WDK 电源管理
- 设备电源 ups WDK 内核
- 开启设备 WDK 内核
- IRP_MN_SET_POWER
- 工作状态返回 WDK 电源管理
- 启用设备 WDK 电源管理
- 自动电源 ups WDK 内核
- 在 power WDK 内核上
- Irp WDK 电源管理
- 启动电源管理 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d2b154c29ce0069de9640d1148727342f457c77
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827632"
---
# <a name="powering-up-a-device"></a>打开设备的电源





当总线驱动程序处理 PnP [**IRP\_MN 时\_启动**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)其某个子设备\_设备请求，则应打开设备并调用[**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)将设备电源状态报告给电源管理器。 设备打开是设备启动的一个隐含部分。 设备电源策略所有者不会发送[**IRP\_MN\_\_设置**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power) **PowerDeviceD0**的电源请求，因此驱动程序应在启动时不会收到这些 irp。

当设备断电以节省电源时，其驱动程序应在 i/o 请求到达时接通电源。 在这种情况下，设备电源策略所有者必须发送**IRP\_MN\_设置\_电源**，以将设备恢复到工作状态。 IRP 完成后，设备的驱动程序将停止排队 i/o 并开始处理队列中的请求。

 

 




