---
title: 非 PnP 驱动程序的 Unload 例程
description: 非 PnP 驱动程序的 Unload 例程
ms.assetid: 5917648f-1e7e-4b39-9aa6-d6cdaac7a2cd
keywords:
- 卸载例程 WDK 内核，非 PnP 驱动程序
- 非即插即用卸载例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9169d44f5b38c6eaaa50ad6686336ec039c7f189
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365456"
---
# <a name="non-pnp-drivers-unload-routine"></a>非 PnP 驱动程序的 Unload 例程





早期驱动程序和高级文件系统驱动程序，它不处理即插即用设备删除请求，必须释放资源、 删除设备对象，并从设备堆栈中分离其[ *Unload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)例程。

如果它具有不这样做，首先要做的旧设备驱动程序应在其*Unload*例程是禁用来自设备的中断。 否则，可能会调用其 ISR 以处理时的设备中断*Unload*例程释放 ISR 需要处理中断的设备扩展中的资源。 即使在这些情况下，成功运行其 ISR [ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)或[ *CustomDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)例程的 ISR 队列和可能在 IRQL 运行其他驱动程序例程&gt;= 调度\_级别之前, 将执行*卸载*例程重新获得控制，从而提高了的可能性， *卸载*例程已删除的资源的另一个驱动程序例程的引用。 请参阅[管理硬件优先级](managing-hardware-priorities.md)有关详细信息。

禁用中断之后, 的文件系统和旧驱动程序必须释放资源和对象。 有关详细信息，请参阅以下两个部分：

[释放驱动程序分配资源](releasing-driver-allocated-resources.md)

[释放设备和控制器对象](releasing-device-and-controller-objects.md)

 

 




