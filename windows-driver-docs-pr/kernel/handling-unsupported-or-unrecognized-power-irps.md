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
ms.openlocfilehash: 9fb0ff5ce96b07e766669b003513a2c91b9eb053
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190681"
---
# <a name="handling-unsupported-or-unrecognized-power-irps"></a>处理不受支持的或无法识别的电源 IRP





如果驱动程序不支持特定电源 IRP，则必须将 IRP 向下传递到下一个较低的驱动程序。 堆栈进一步向下的驱动程序可能已准备好处理 IRP，并且必须有机会执行此操作。

若要传递不支持或无法识别的 power IRP，驱动程序应按照 [通过电源 irp](passing-power-irps.md)中所述的顺序调用以下例程：

-   在 Windows 7 和 Windows Vista 中，调用 [**IoSkipCurrentIrpStackLocation**](./mm-bad-pointer.md) 和 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)。

-   在 Windows Server 2003、Windows XP 和 Windows 2000 中，调用 [**PoStartNextPowerIrp**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)、 **IoSkipCurrentIrpStackLocation**和 [**PoCallDriver**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)。

在将 IRP 向下传递到设备堆栈之前，驱动程序不应更改 IRP 中的任何内容。

 

