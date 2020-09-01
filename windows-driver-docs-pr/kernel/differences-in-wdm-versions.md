---
title: WDM 版本的差异
description: WDM 版本的差异
ms.assetid: 735b01c4-4eff-4c8e-ab60-3813d1830112
keywords:
- WDM 驱动程序 WDK 内核，版本
- 版本 WDK WDM
- 兼容性 WDK WDM
- 跨系统兼容性 WDK WDM
- 即插即用 WDK WDM
- 驱动程序支持例程 WDK WDM
- 电源管理 WDK WDM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c43c282090002cc33d6d6ca2baf00637f2098332
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191863"
---
# <a name="differences-in-wdm-versions"></a>WDM 版本的差异





确保跨系统兼容性的最简单方法是编写一个驱动程序，该驱动程序只使用由最小编号的 WDM 版本支持的功能。 但这并不总是可行。 有时，驱动程序需要额外的代码才能利用在更新后的 WDM 版本中提供的功能，或对 Windows 操作系统之间的差异进行补偿。

### <a name="wdm-differences-in-driver-support-routines"></a>驱动程序支持例程中的 WDM 差异

每个 [驱动程序支持例程](/windows-hardware/drivers/ddi/index) 的 Windows 驱动程序工具包 (WDK) 参考页指示例程是否限制为特定版本的 WDM，或者其行为在不同的操作系统版本上是否不同。 在跨系统驱动程序中使用任何驱动程序支持例程之前，请务必了解任何特定于版本的限制或行为。

### <a name="wdm-differences-in-plug-and-play"></a>即插即用中的 WDM 差异

以下即插即用 i/o 请求包 (IRP) 仅在) 1.10 (基于 NT 的 Windows 2000 和更高版本的 Windows 和更高版本中受支持。

[**IRP \_ MN \_ 意外 \_ 删除**](./irp-mn-surprise-removal.md)

此外，在 Windows 98/Me 上，以下 Irp 的工作方式与在基于 NT 的操作系统上的工作方式不同：

[**IRP \_MN \_ 停止 \_ 设备**](./irp-mn-stop-device.md)和[ **IRP \_ MN \_ 删除 \_ 设备**](./irp-mn-remove-device.md)

[**IRP \_ MN \_ 查询 \_ 删除 \_ 设备**](./irp-mn-query-remove-device.md)

### <a name="wdm-differences-in-power-management"></a>电源管理中的 WDM 差异

以下电源管理功能和 i/o 请求在 Windows 98/Me 操作系统和基于 NT 的操作系统之间的操作上有所不同：

[**PoSetPowerState**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)

[**PoRequestPowerIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)

[**PoRegisterDeviceForIdleDetection**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poregisterdeviceforidledetection)

[**IRP \_ MN \_ 查询 \_ 能力**](./irp-mn-query-power.md)

[**IRP \_ MN \_ 设置 \_ 电源**](./irp-mn-set-power.md)

完成电源 Irp 后，Windows 98/Me 上的驱动程序必须以 IRQL = 被动级别完成电源 Irp \_ ，而基于 NT 的操作系统上的驱动程序可以以 irql = 被动 \_ 级别或 IRQL = 调度级别完成此类 irp \_ 。

与 \_ \_ 基于 NT 的操作系统相比，在 Windows 98/Me 操作系统上， [**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object) 结构中的 DO POWER PAGABLE 标志的使用方式不同。

### <a name="wdm-differences-in-kernel-mode-driver-operation"></a>内核模式驱动程序操作中的 WDM 差异

适用于 Windows 98/Me 的内核模式 WDM 驱动程序必须遵循有关使用浮点运算、MMX、3DNOW！或 Intel 的 SSE 扩展的某些准则。 有关详细信息，请参阅 [在 WDM 驱动程序中使用浮点或 MMX](using-floating-point-or-mmx-in-a-wdm-driver.md)。

Windows 98/Me 提供了固定数量的工作线程，这些线程可能不适合某些驱动程序。

 

