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
ms.openlocfilehash: 3d44dc520ab0e86eb200a8b5b9a9e3f2ec574113
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838737"
---
# <a name="differences-in-wdm-versions"></a>WDM 版本的差异





确保跨系统兼容性的最简单方法是编写一个驱动程序，该驱动程序只使用由最小编号的 WDM 版本支持的功能。 但这并不总是可行。 有时，驱动程序需要额外的代码才能利用在更新后的 WDM 版本中提供的功能，或对 Windows 操作系统之间的差异进行补偿。

### <a name="wdm-differences-in-driver-support-routines"></a>驱动程序支持例程中的 WDM 差异

每个[驱动程序支持例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)的 "Windows 驱动程序工具包（WDK）参考" 页指示例程是否限制为特定版本的 WDM，或者其行为在不同的操作系统版本上是否不同。 在跨系统驱动程序中使用任何驱动程序支持例程之前，请务必了解任何特定于版本的限制或行为。

### <a name="wdm-differences-in-plug-and-play"></a>即插即用中的 WDM 差异

仅 Windows 2000 和更高版本的基于 NT 的操作系统（WDM 版本1.10 及更高版本）支持以下即插即用 i/o 请求数据包（IRP）：

[**IRP\_MN\_意外\_删除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)

此外，在 Windows 98/Me 上，以下 Irp 的工作方式与在基于 NT 的操作系统上的工作方式不同：

[**Irp\_MN\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)和[ **IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)

[**IRP\_MN\_查询\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)

### <a name="wdm-differences-in-power-management"></a>电源管理中的 WDM 差异

以下电源管理功能和 i/o 请求在 Windows 98/Me 操作系统和基于 NT 的操作系统之间的操作上有所不同：

[**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)

[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)

[**PoRegisterDeviceForIdleDetection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poregisterdeviceforidledetection)

[**IRP\_MN\_QUERY\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)

[**IRP\_MN\_集\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)

完成电源 Irp 后，Windows 98/Me 上的驱动程序必须以 IRQL = 被动\_级别完成电源 Irp，而基于 NT 的操作系统上的驱动程序可以在 IRQL = 被动\_级别或 IRQL = 调度\_级别完成此类 Irp。

[**设备\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)结构中的 DO\_POWER\_PAGABLE 标志在 Windows 98/Me 操作系统上的使用方式与基于 NT 的操作系统上的使用方式不同。

### <a name="wdm-differences-in-kernel-mode-driver-operation"></a>内核模式驱动程序操作中的 WDM 差异

适用于 Windows 98/Me 的内核模式 WDM 驱动程序必须遵循有关使用浮点运算、MMX、3DNOW！或 Intel 的 SSE 扩展的某些准则。 有关详细信息，请参阅[在 WDM 驱动程序中使用浮点或 MMX](using-floating-point-or-mmx-in-a-wdm-driver.md)。

Windows 98/Me 提供了固定数量的工作线程，这些线程可能不适合某些驱动程序。

 

 




