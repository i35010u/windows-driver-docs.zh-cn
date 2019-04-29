---
title: 启动设备的设计指导原则
description: 启动设备的设计指导原则
ms.assetid: fbdde107-f3a5-4713-a4ac-1c9bafa3c634
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a82ff0a188147bbe034728fc2a372b7069948182
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388186"
---
# <a name="design-guidelines-for-starting-devices"></a>启动设备的设计指导原则





-   PnP 管理器失败创建请求的设备，直到[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749) IRP 完成后，该值指示该设备的所有驱动程序已执行了其开始操作。

-   因为[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程在 IRQL 被动在系统线程的上下文中运行\_级别，与分配任何内存[ **ExAllocatePoolWithTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544520)在初始化过程中以独占方式使用可以是从页面缓冲池，只要该驱动程序不会控制保存系统页面文件的设备。 必须随此类内存分配[ **ExFreePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544590)之前*DispatchPnP*例程将返回控制。

-   WDM 设备驱动程序的 ISR 应该能够确定是否已调用与虚假中断甚至在设备启动过程。 在从调用返回[ **IoConnectInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/ff548371)处理的代码路径中**IRP\_MN\_启动\_设备**，ISR可以调用立即如果在设备上启用了中断。

 

 




