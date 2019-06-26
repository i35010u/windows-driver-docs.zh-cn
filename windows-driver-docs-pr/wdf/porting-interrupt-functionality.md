---
title: 移植中断
description: 移植中断
ms.assetid: E91B971D-044C-45A4-AD76-44AFB1213F8E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dae585ccb665feea1d245439cb31ac7f7c32bfb8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379633"
---
# <a name="porting-interrupts"></a>移植中断


支持和服务中断的代码是在 WDF 和 WDM 驱动程序类似。 还有一个主要区别：

-   WDF 驱动程序创建 WDFINTERRUPT 对象并将其中断服务例程 (ISR) 回调注册通过调用[ **WdfInterruptCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)从其[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调。
-   WDM 驱动程序创建 KINTERRUPT 结构，并连接期间对其[ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)处理。

[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) WDF 驱动程序中的回调执行相同的任务作为 WDM 驱动程序[ *InterruptService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kservice_routine)例程。 *EvtInterruptIsr*回调调用[ **WdfInterruptQueueDpcForIsr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueuedpcforisr)到队列[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)供以后处理在调度回调\_级别。 在响应中，框架将 DPC 对象添加到运行此回调系统队列。

有关框架中断对象的详细信息，请参阅[处理硬件中断](handling-hardware-interrupts.md)。

 

 





