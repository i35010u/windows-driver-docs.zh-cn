---
title: 移植中断
description: 移植中断
ms.assetid: E91B971D-044C-45A4-AD76-44AFB1213F8E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e90106be0a01fafe5832b70ea91db87b17ff5d7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842251"
---
# <a name="porting-interrupts"></a>移植中断


支持和维护中断的代码在 WDF 和 WDM 驱动程序中是类似的。 主要区别在于：

-   WDF 驱动程序创建 WDFINTERRUPT 对象，并通过从其[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调调用[**WdfInterruptCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)来注册其中断服务例程（ISR）回调。
-   WDM 驱动程序创建 KINTERRUPT 结构，并在[**IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)处理过程中将其连接。

WDF 驱动程序中的[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)回调执行与 WDM 驱动程序的[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)例程相同的任务。 *EvtInterruptIsr*回调调用[**WdfInterruptQueueDpcForIsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueuedpcforisr)将[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调排队，以便以后在调度\_级别进行处理。 在响应中，框架将一个 DPC 对象添加到运行此回调的系统队列。

有关框架中断对象的详细信息，请参阅[处理硬件中断](handling-hardware-interrupts.md)。

 

 





