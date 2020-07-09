---
title: 维护中断（UMDF 1）
description: 为中断提供服务
ms.assetid: 79BA75B3-E10F-4AC1-A2C5-A502BF821188
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b70a4890494814ce597e9867561cd7e03567dc7
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141266"
---
# <a name="servicing-an-interrupt-umdf-1"></a>维护中断（UMDF 1）


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

为中断提供服务包括两个步骤：

1.  在中断服务例程中快速保存易失性信息（如注册内容）。
2.  处理工作项例程中保存的可变信息。

当设备生成硬件中断时，框架会调用驱动程序的中断服务例程（ISR），这是基于框架的驱动程序作为[*OnInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr)回调函数实现的。

在被动级别运行的[*OnInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr)回调函数 \_ 必须快速保存中断信息，如注册内容、对工作项进行排队以便进一步处理数据，并从 ISR 返回，以允许在中断行共享时处理其他中断。 由于 UMDF 驱动程序的 ISR 在被动 \_ 级别运行，因此不建议处理基于 PCI 线路的中断。 通常会在多个设备之间共享这些中断，其中一些中断可能不会接受 ISR 延迟。 但是，可以在 UMDF 驱动程序中处理 PCI MSI 中断。 这些中断具有边缘语义并且不共享。

通常， [*OnInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr)回调函数会安排一个工作项，以便以后处理保存的信息。 基于框架的驱动程序将工作项例程作为[*OnInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_workitem)回调函数实现。

大多数驱动程序对每种类型的中断使用单个[*OnInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_workitem)回调函数。 若要计划*OnInterruptWorkItem*回调函数的执行，驱动程序必须从[*OnInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr)回调函数内调用[**IWDFInterrupt：： QueueWorkItemForIsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-queueworkitemforisr) 。

如果你的驱动程序为每个设备创建多个框架队列对象，则可以考虑对每个队列使用单独的工作项对象和[*OnWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfworkitem/nc-wudfworkitem-wudf_workitem_function)回调函数。 若要计划*OnWorkItem*回调函数的执行，驱动程序必须首先通过调用[**IWdfDevice3：： CreateWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createworkitem)（通常来自驱动程序的[**IDriverEntry：： OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)回调函数）来创建一个或多个工作项对象。 然后，驱动程序的[*OnInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr)回调函数可以调用[**IWDFWorkItem：：排队**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfworkitem-enqueue)。

驱动程序通常会在其[*OnInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_workitem)或[*OnWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfworkitem/nc-wudfworkitem-wudf_workitem_function)回调函数中完成 i/o 请求。

有关处理中断的 UMDF 驱动程序的示例，请参阅[SpbAccelerometer](https://go.microsoft.com/fwlink/p/?linkid=256189)示例驱动程序，可从 WINDOWS 8 WDK 开始使用。

 

 





