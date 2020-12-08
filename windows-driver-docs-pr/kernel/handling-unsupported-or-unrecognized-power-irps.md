---
title: 处理不受支持的或无法识别的电源 IRP
description: 处理不受支持的或无法识别的电源 IRP
keywords:
- power Irp WDK 内核，不受支持
- 不支持的 power Irp WDK 内核
- 无法识别的 power Irp WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: aab4cddd2d45087cbe2108029e01898b724eb115
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813049"
---
# <a name="handling-unsupported-or-unrecognized-power-irps"></a>处理不受支持的或无法识别的电源 IRP





如果驱动程序不支持特定电源 IRP，则必须将 IRP 向下传递到下一个较低的驱动程序。 堆栈进一步向下的驱动程序可能已准备好处理 IRP，并且必须有机会执行此操作。

若要传递不支持或无法识别的 power IRP，驱动程序应按照 [通过电源 irp](passing-power-irps.md)中所述的顺序调用以下例程：

-   在 Windows 7 和 Windows Vista 中，调用 [**IoSkipCurrentIrpStackLocation**](./mm-bad-pointer.md) 和 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)。

-   在 Windows Server 2003、Windows XP 和 Windows 2000 中，调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)、 **IoSkipCurrentIrpStackLocation** 和 [**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)。

在将 IRP 向下传递到设备堆栈之前，驱动程序不应更改 IRP 中的任何内容。

 

