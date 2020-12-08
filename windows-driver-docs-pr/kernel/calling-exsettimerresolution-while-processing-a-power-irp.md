---
title: 处理电源 IRP 时调用 ExSetTimerResolution
description: 处理电源 IRP 时调用 ExSetTimerResolution
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9e49680ff435c43ad454c256491d79d51157f197
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816155"
---
# <a name="calling-exsettimerresolution-while-processing-a-power-irp"></a>处理电源 IRP 时调用 ExSetTimerResolution


在处理 [**IRP \_ MJ \_ 电源**](./irp-mj-power.md) 请求的过程中，电源管理器持有一个资源上的锁， [**ExSetTimerResolution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimerresolution) 必须获取该资源才能完成。 因此，如果驱动程序在处理电源请求时直接或间接调用此例程，然后等待对例程的调用在驱动程序完成电源请求之前返回，则会发生死锁。 处理 power request 时，只有当驱动程序在完成电源请求之前不会等待调用此例程返回时，驱动程序才能安全地调用 **ExSetTimerResolution** 。 例如，驱动程序可以创建调用 **ExSetTimerResolution** 的工作线程，前提是该驱动程序随后完成了电源请求，而无需等待调用此例程。

 

