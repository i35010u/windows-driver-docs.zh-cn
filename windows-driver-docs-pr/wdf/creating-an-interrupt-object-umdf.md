---
title: " (UMDF 1) 创建中断对象"
description: 创建中断对象
ms.assetid: D281F2E8-3ADA-4F4E-B345-CE72FA3C69EC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaeed554b71828852ec81ca3009677f842e04185
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185540"
---
# <a name="creating-an-interrupt-object-umdf-1"></a> (UMDF 1) 创建中断对象


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

处理设备硬件中断的 UMDF 驱动程序必须为每个设备可以支持的每个中断创建一个框架中断对象。

通常，驱动程序会在 [**IDriverEntry：： OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)中创建框架中断对象。 但是，还可以在 [**IPnpCallbackHardware2：： OnPrepareHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)中创建中断对象。

若要创建框架中断对象，驱动程序必须初始化 [**WUDF \_ 中断 \_ 配置**](/windows-hardware/drivers/ddi/wudfinterrupt/ns-wudfinterrupt-_wudf_interrupt_config) 结构，并将其传递给 [**IWDFDevice3：： CreateInterrupt**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt) 方法。 此方法注册以下驱动程序提供的事件回调函数：

<a href="" id="oninterruptenable"></a>[*OnInterruptEnable*](/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable)  
启用硬件中断。

<a href="" id="oninterruptdisable"></a>[*OnInterruptDisable*](/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_disable)  
禁用硬件中断。

<a href="" id="oninterruptisr"></a>[*OnInterruptIsr*](/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr)  
中断服务例程 (ISR) 用于中断。

<a href="" id="oninterruptworkitem"></a>[*OnInterruptWorkItem*](/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_workitem)  
中断的辅助进程例程。

或者，驱动程序可以调用 [**IWDFInterrupt：： SetPolicy**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-setpolicy) 或 [**IWDFInterrupt：： SetExtendedPolicy**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-setextendedpolicy) 来指定其他中断参数。

在即插即用 (PnP) manager 将系统资源（如中断向量）分配给设备之前，框架将调用驱动程序的 [**IDriverEntry：： OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd) 回调函数。 PnP 管理器分配资源后，框架会在设备的中断对象中存储中断资源。  (不支持即插即用的驱动程序无法使用中断对象。 ) 

在 Windows Vista 和更高版本的操作系统中， (Msi) 支持消息信号中断。 若要使操作系统支持设备的 Msi，驱动程序的 INF 文件必须在注册表中设置一些值。 有关如何设置这些值的信息，请参阅 [启用注册表中的消息终止中断](../kernel/enabling-message-signaled-interrupts-in-the-registry.md)。

如果设备可以支持特定数量的 MSI 消息，则 PnP 管理器会尝试将该数量的消息分配到设备。 如果 PnP 管理器无法分配设备可以支持的所有消息，它将仅向设备分配一条消息。

驱动程序应为设备可以支持的每个中断矢量或 MSI 消息创建框架中断对象。 如果 PnP 管理器未向设备授予设备能够支持的所有中断资源，则不会使用额外的中断对象，也不会调用其回调函数。

 

