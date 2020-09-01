---
title: 非 PnP 驱动程序的 Unload 例程
description: 非 PnP 驱动程序的 Unload 例程
ms.assetid: 5917648f-1e7e-4b39-9aa6-d6cdaac7a2cd
keywords:
- 卸载例程 WDK 内核，非 PnP 驱动程序
- 非 PnP 卸载例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bb19cf12b8338efe2bb6f07c6a359a7b4b7689a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191355"
---
# <a name="non-pnp-drivers-unload-routine"></a>非 PnP 驱动程序的 Unload 例程





较早的驱动程序和高级文件系统驱动程序（不处理 PnP 设备删除请求）必须释放资源、删除设备对象，以及在其 [*卸载*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 例程中分离出设备堆栈。

如果尚未执行此操作，那么旧式设备驱动程序在其 *卸载* 例程中应执行的第一件事是禁用设备的中断。 否则，可以调用其 ISR 来处理设备中断，同时 *卸载* 例程会释放 isr 需要处理中断的设备扩展中的资源。 即使在这种情况下，它的 ISR 成功运行， [*CustomDpc*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)但在[*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine) &gt; \_ *卸载*例程重新获得控制之前*Unload* ，ISR 队列和可能运行的其他驱动程序例程（也可能是以 IRQL = 调度级别运行）的 DpcForIsr 或 CustomDpc 有关详细信息，请参阅 [管理硬件优先级](managing-hardware-priorities.md) 。

禁用中断后，文件系统和旧驱动程序必须释放资源和对象。 有关详细信息，请参阅以下两部分：

[释放驱动程序分配的资源](releasing-driver-allocated-resources.md)

[释放设备和控制器对象](releasing-device-and-controller-objects.md)

 

