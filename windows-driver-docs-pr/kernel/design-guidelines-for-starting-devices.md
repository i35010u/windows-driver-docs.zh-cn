---
title: 启动设备的设计指导原则
description: 启动设备的设计指导原则
ms.assetid: fbdde107-f3a5-4713-a4ac-1c9bafa3c634
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 429e61e8ecd9b7ff172d60efed4c8765fa38a081
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836941"
---
# <a name="design-guidelines-for-starting-devices"></a>启动设备的设计指导原则





-   PnP 管理器无法创建设备请求，直到[**irp\_MN\_START\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)IRP 完成为止，这表明设备的所有驱动程序都已执行了其启动操作。

-   由于[*DispatchPnP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程在具有 IRQL 被动\_级别的系统线程的上下文中运行，因此在初始化期间使用[**ExAllocatePoolWithTag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)分配的任何内存都可以从分页池中进行，只要该驱动程序不控制包含系统页面文件的设备。 在*DispatchPnP*例程返回 control 之前，必须使用[**ExFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)释放此类内存分配。

-   WDM 设备驱动程序的 ISR 应该能够确定是否已通过虚假中断来调用它，即使在设备启动期间也是如此。 当在处理**IRP\_MN\_启动\_设备**的代码路径中调用[**IoConnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)时，如果在设备上启用了中断，则可以立即调用 ISR。

 

 




