---
title: 正在同步 (UMDF 1) 的中断代码
description: 同步中断代码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e442137d9d937b69d722885249b743cb0de887d3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815561"
---
# <a name="synchronizing-interrupt-code-umdf-1"></a>正在同步 (UMDF 1) 的中断代码


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

所有访问中断数据缓冲区的驱动程序代码都必须进行同步，以便一次只有一个例程访问数据。

可以通过使用手动中断锁定或自动回叫序列化来同步中断代码。

## <a name="manual-interrupt-locking"></a>手动中断锁定


在调用 [*OnInterruptIsr*](/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr)、 [*OnInterruptDisable*](/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_disable)或 [*OnInterruptEnable*](/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_enable) 回调之前，UMDF 将获取中断锁。

如果驱动程序需要使用中断锁来同步任何代码，它将调用 [**IWDFInterrupt：： AcquireInterruptLock**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-acquireinterruptlock) 和 [**IWDFInterrupt：： ReleaseInterruptLock**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-releaseinterruptlock)。 例如，驱动程序通过使用这些方法，在其 [*OnInterruptWorkItem*](/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_workitem) 回调例程中获取并释放中断锁。 但是，在 i/o 调度回调 (如 [**OnRead**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackread-onread) 和 [**OnWrite**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackwrite-onwrite)) 中，驱动程序首先调用 [**IWDFInterrupt：： TryToAcquireInterruptLock**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-trytoacquireinterruptlock) 来决定是将工作项排队还是在同一线程中完成工作，以避免潜在的死锁。 有关可通过任意线程上下文调用 **IWDFInterrupt：： AcquireInterruptLock** 引起的死锁方案示例，请参阅 [**IWDFInterrupt：： AcquireInterruptLock**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-acquireinterruptlock)的 "备注" 部分。

如果 [**IWDFInterrupt：： TryToAcquireInterruptLock**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-trytoacquireinterruptlock) 返回 **TRUE**，则驱动程序已在同一线程中获取中断锁。 在这种情况下，驱动程序执行需要该锁定的工作，然后调用 [**ReleaseInterruptLock**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfinterrupt-releaseinterruptlock)。 如果 **IWDFInterrupt：： TryToAcquireInterruptLock** 返回 **FALSE**，则驱动程序会将工作项排队，并在其 [*OnWorkItem*](/windows-hardware/drivers/ddi/wudfworkitem/nc-wudfworkitem-wudf_workitem_function) 回调中执行工作。 在这种情况下，工作项不能使用自动序列化。

## <a name="using-automatic-serialization"></a>使用自动序列化


UMDF 驱动程序可以通过调用 [**IWDFDeviceInitialize：： SetLockingConstraint**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setlockingconstraint) ，并将 *LockType* 参数设置为 **WdfDeviceLevel**，来请求自动回拨同步。

然后，在调用 [**CreateInterrupt**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-createinterrupt)之前，驱动程序将其 [**WUDF \_ 中断 \_ 配置**](/windows-hardware/drivers/ddi/wudfinterrupt/ns-wudfinterrupt-_wudf_interrupt_config)结构的 **AutomaticSerialization** 成员设置为 **TRUE** 。

因此，UMDF 使用 i/o 队列、请求取消和文件对象回调例程序列化驱动程序的 [*OnInterruptWorkItem*](/windows-hardware/drivers/ddi/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_workitem) 回调。 在这种情况下，UMDF 使用回调锁，而不是按中断对象锁。

 

