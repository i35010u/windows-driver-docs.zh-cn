---
title: 处理电源 IRP 时调用 ExSetTimerResolution
description: 处理电源 IRP 时调用 ExSetTimerResolution
ms.assetid: 999a76ab-1586-4157-bfa7-8cc5dd517c71
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a0e7e496b46ad506e72791139948aab13ad9b086
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837174"
---
# <a name="calling-exsettimerresolution-while-processing-a-power-irp"></a>处理电源 IRP 时调用 ExSetTimerResolution


在处理[**IRP\_MJ\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)请求的过程中，电源管理器会持有[**ExSetTimerResolution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimerresolution)必须获取的资源的锁。 因此，如果驱动程序在处理电源请求时直接或间接调用此例程，然后等待对例程的调用在驱动程序完成电源请求之前返回，则会发生死锁。 处理 power request 时，只有当驱动程序在完成电源请求之前不会等待调用此例程返回时，驱动程序才能安全地调用**ExSetTimerResolution** 。 例如，驱动程序可以创建调用**ExSetTimerResolution**的工作线程，前提是该驱动程序随后完成了电源请求，而无需等待调用此例程。

 

 




