---
title: 基于 GPIO 的中断资源
description: 发送到通用 I/O (GPIO) 插针中断获取作为抽象 Windows GPIO 中断的外围设备的驱动程序中断资源。
ms.assetid: 65031C43-917D-4665-BD7F-97D3DDA0A918
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4faac9f588b4980abb7094d4c13895603f342b9e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326147"
---
# <a name="gpio-based-interrupt-resources"></a>基于 GPIO 的中断资源


发送到通用 I/O (GPIO) 插针中断获取作为抽象 Windows GPIO 中断的外围设备的驱动程序中断资源。 [内核模式驱动程序框架](https://msdn.microsoft.com/library/windows/hardware/ff544296)(KMDF) 驱动程序和[用户模式驱动程序框架](../wdf/overview-of-the-umdf.md)(UMDF) 驱动程序收到这些资源通过其[ *EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)事件回调函数。

使用基于 GPIO 的中断资源的外围设备驱动程序可以忽略低级别实施详细信息，例如是否中断中断控制器或处理器芯片上一个中断插针生成通过而不是 GPIO pin。

基于 GPIO 的中断是一种资源类型的**CmResourceTypeInterrupt**。 中包含此中断的配置参数**u.Interrupt**的成员[ **CM\_部分\_资源\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff541977)结构，它描述中断资源。 若要连接到中断的中断服务例程 (ISR)，UMDF 或 KMDF 驱动程序提供两者[原始和已翻译](https://msdn.microsoft.com/library/windows/hardware/ff544561)中断创建方法中断资源的说明。

外围设备的 KMDF 或 UMDF 驱动程序调用[ **WdfInterruptCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)方法以从设备连接到中断的 ISR。 此方法的输入参数之一是一个指向[ **WDF\_中断\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)结构，其中包含中断的配置信息。 有关详细信息，请参阅[处理硬件中断](../wdf/handling-hardware-interrupts.md)。

如果外围设备驱动程序使用多个 GPIO 中断资源，此驱动程序必须了解这些资源作为输入参数提供的原始和已翻译资源列表中的显示的顺序*EvtDevicePrepareHardware*函数或**OnPrepareHardware**方法。 这些列表中的资源显示的顺序必须匹配所需的驱动程序的平台固件中介绍的顺序。

 

 




