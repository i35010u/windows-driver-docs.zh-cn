---
title: 处理不受支持的或无法识别的电源 IRP
description: 处理不受支持的或无法识别的电源 IRP
ms.assetid: 0664389c-f746-4025-969f-8c3b07139026
keywords:
- power Irp WDK 内核，不受支持
- 不支持的 power Irp WDK 内核
- 无法识别的 power Irp WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a38190e369f7df027723adc8d3424d7a653299b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836479"
---
# <a name="handling-unsupported-or-unrecognized-power-irps"></a>处理不受支持的或无法识别的电源 IRP





如果驱动程序不支持特定电源 IRP，则必须将 IRP 向下传递到下一个较低的驱动程序。 堆栈进一步向下的驱动程序可能已准备好处理 IRP，并且必须有机会执行此操作。

若要传递不支持或无法识别的 power IRP，驱动程序应按照[通过电源 irp](passing-power-irps.md)中所述的顺序调用以下例程：

-   在 Windows 7 和 Windows Vista 中，调用[**IoSkipCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)和[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)。

-   在 Windows Server 2003、Windows XP 和 Windows 2000 中，调用[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)、 **IoSkipCurrentIrpStackLocation**和[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)。

在将 IRP 向下传递到设备堆栈之前，驱动程序不应更改 IRP 中的任何内容。

 

 




