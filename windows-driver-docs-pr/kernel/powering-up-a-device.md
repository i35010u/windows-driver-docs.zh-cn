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
ms.openlocfilehash: cc1ef2ed7be8d4f3917e7bedd9fe74754b78a6f9
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188223"
---
# <a name="powering-up-a-device"></a>打开设备的电源





当总线驱动程序处理其某个子设备的 PnP [**IRP \_ MN \_ 开始 \_ 设备**](./irp-mn-start-device.md) 请求时，它应接通设备电源，并调用 [**PoSetPowerState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate) 来向电源管理器报告设备电源状态。 设备打开是设备启动的一个隐含部分。 设备电源策略所有者不会为**PowerDeviceD0**发送[**IRP \_ MN \_ 设置 \_ 电源**](./irp-mn-set-power.md)请求，因此驱动程序应在启动时不会收到这些 irp。

当设备断电以节省电源时，其驱动程序应在 i/o 请求到达时接通电源。 在这种情况下，设备电源策略所有者必须发送 **IRP \_ MN \_ 集 \_ 电源** ，以将设备恢复到工作状态。 IRP 完成后，设备的驱动程序将停止排队 i/o 并开始处理队列中的请求。

 

