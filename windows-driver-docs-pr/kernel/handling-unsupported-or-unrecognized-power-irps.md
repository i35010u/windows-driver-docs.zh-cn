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
ms.openlocfilehash: d6e8fb7f12329e0551df306a638a7a73d9db0f87
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371901"
---
# <a name="handling-unsupported-or-unrecognized-power-irps"></a>处理不受支持的或无法识别的电源 IRP





如果驱动程序不支持特定电源 IRP，它必须不过将向设备堆栈下的 IRP 传递给下一个较低驱动程序。 驱动程序进一步在堆栈的下层可能准备好处理 IRP，并且必须具有执行此操作的机会。

若要传递不受支持或无法识别 power IRP，驱动程序应调用以下例程中所述的顺序[传递 Power Irp](passing-power-irps.md):

-   在 Windows 7 和 Windows Vista 中，调用[ **IoSkipCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)并[ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)。

-   在 Windows Server 2003、 Windows XP 和 Windows 2000 中，调用[ **PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-postartnextpowerirp)， **IoSkipCurrentIrpStackLocation**，以及[ **PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)。

驱动程序不应更改任何 IRP 传递 IRP 下设备堆栈之前。

 

 




