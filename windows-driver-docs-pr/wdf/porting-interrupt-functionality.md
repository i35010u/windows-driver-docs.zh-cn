---
title: 移植中断
description: 移植中断
ms.assetid: E91B971D-044C-45A4-AD76-44AFB1213F8E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1642864a7816681ceecc8d4ab044dfd06b78dc09
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390093"
---
# <a name="porting-interrupts"></a>移植中断


支持和服务中断的代码是在 WDF 和 WDM 驱动程序类似。 还有一个主要区别：

-   WDF 驱动程序创建 WDFINTERRUPT 对象并将其中断服务例程 (ISR) 回调注册通过调用[ **WdfInterruptCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547345)从其[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调。
-   WDM 驱动程序创建 KINTERRUPT 结构，并连接期间对其[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)处理。

[ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735) WDF 驱动程序中的回调执行相同的任务作为 WDM 驱动程序[ *InterruptService* ](https://msdn.microsoft.com/library/windows/hardware/ff547958)例程。 *EvtInterruptIsr*回调调用[ **WdfInterruptQueueDpcForIsr** ](https://msdn.microsoft.com/library/windows/hardware/ff547371)到队列[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)供以后处理在调度回调\_级别。 在响应中，框架将 DPC 对象添加到运行此回调系统队列。

有关框架中断对象的详细信息，请参阅[处理硬件中断](handling-hardware-interrupts.md)。

 

 





