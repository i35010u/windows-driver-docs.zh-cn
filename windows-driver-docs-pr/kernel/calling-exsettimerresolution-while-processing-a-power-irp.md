---
title: 处理电源 IRP 时调用 ExSetTimerResolution
description: 处理电源 IRP 时调用 ExSetTimerResolution
ms.assetid: 999a76ab-1586-4157-bfa7-8cc5dd517c71
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3894a5cb7fb3f7b30db8c79c29bd780a84fc2e63
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188645"
---
# <a name="calling-exsettimerresolution-while-processing-a-power-irp"></a>处理电源 IRP 时调用 ExSetTimerResolution


在处理 [**IRP \_ MJ \_ 电源**](./irp-mj-power.md) 请求的过程中，电源管理器持有一个资源上的锁， [**ExSetTimerResolution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimerresolution) 必须获取该资源才能完成。 因此，如果驱动程序在处理电源请求时直接或间接调用此例程，然后等待对例程的调用在驱动程序完成电源请求之前返回，则会发生死锁。 处理 power request 时，只有当驱动程序在完成电源请求之前不会等待调用此例程返回时，驱动程序才能安全地调用 **ExSetTimerResolution** 。 例如，驱动程序可以创建调用 **ExSetTimerResolution**的工作线程，前提是该驱动程序随后完成了电源请求，而无需等待调用此例程。

 

