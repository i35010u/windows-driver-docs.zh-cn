---
title: DPC 对象简介
description: DPC 对象简介
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 26c14834d42237edcebf87fd1a0a9481dfbf4de9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833423"
---
# <a name="introduction-to-dpc-objects"></a>DPC 对象简介





由于 Isr 必须尽可能快地执行，因此，驱动程序通常必须在 ISR 返回后，为中断提供服务。 因此，系统将支持 (Dpc) 的 *延迟过程调用* ，该调用可以从 isr 排队，并在更高的 IRQL 下执行，且比 ISR 更低。

每个 DPC 都与一个系统定义的 *dpc 对象* 相关联。 系统为每个设备对象提供一个 DPC 对象。 当驱动程序注册一个称为 [*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine) 例程的 dpc 例程时，系统将初始化此 dpc 对象。 如果需要多个 DPC，则驱动程序可以创建其他 DPC 对象。 这些额外的 Dpc 称为 [*CustomDpc*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine) 例程。

驱动程序不应直接引用 DPC 对象内容。 不记录对象的结构。 驱动程序无法访问分配给每个设备对象的系统提供的 DPC 对象。 驱动程序为其他 Dpc 分配存储，但这些 DPC 对象的内容只能由系统例程引用。

DPC 对象和 Dpc 还可与计时器一起使用。 有关详细信息，请参阅 [Timer 对象和 dpc](timer-objects-and-dpcs.md)。

 

