---
title: 设置和使用设备队列
description: 设置和使用设备队列
keywords:
- 设备队列 WDK Irp，设置
- 设备队列 WDK Irp，对象
- 在队列中插入 Irp
- 存储设备队列对象
- 补充 IRP 队列 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b0a4eab3ed1e5d41fdefbb9c16b18942aed35d6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837975"
---
# <a name="setting-up-and-using-device-queues"></a>设置和使用设备队列





驱动程序通过在驱动程序或设备初始化时调用 [**KeInitializeDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedevicequeue) 来设置设备队列对象。 启动其设备 (的) 后，驱动程序将通过调用 [**KeInsertDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertdevicequeue) 或 [**KeInsertByKeyDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinsertbykeydevicequeue)将 irp 插入此队列。 下图说明了这些调用。

![设置和使用设备队列](images/3devqobj.png)

如图所示，驱动程序必须为必须驻留的设备队列对象提供存储。 设置设备队列对象的驱动程序通常在驱动程序创建的设备对象的 [设备扩展](device-extensions.md) 中提供必要的存储，但如果驱动程序使用 [控制器对象](./introduction-to-controller-objects.md) 或由驱动程序分配的非分页池，则存储可以位于控制器扩展中。

如果驱动程序为设备扩展中的设备队列对象提供存储，则它会在创建设备对象之后和启动设备之前调用 **KeInitializeDeviceQueue** 。 换句话说，驱动程序可以从其 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程初始化队列，也可以在处理 PnP [**IRP \_ MN \_ 启动 \_ 设备**](./irp-mn-start-device.md) 请求时对其进行初始化。 在对 **KeInitializeDeviceQueue** 的调用中，驱动程序向设备队列对象传递一个指向它所提供的存储的指针。

在 (的) 启动其设备后，该驱动程序可以通过调用 **KeInsertDeviceQueue** 将 irp 插入其设备队列，后者将 irp 置于队列的尾部，或 **KeInsertByKeyDeviceQueue**，后者根据驱动程序确定的排序 *关键字* 值将 irp 放入队列中，如上图所示。

其中每个支持例程都将返回一个布尔值，指示 IRP 是否已插入队列。 如果队列当前为空，则每个调用还会将设备队列对象的状态设置为 "繁忙"， (不忙) 。 但是，如果队列为空 (不忙) ，则 **KeInsert *Xxx* DEVICEQUEUE** 例程将 IRP 插入到队列中。 相反，它会将设备队列对象的状态设置为 "繁忙" 并返回 **FALSE**。 由于 IRP 尚未排队，因此驱动程序必须将其传递到另一个驱动程序例程以便进一步处理。

**设置补充设备队列时，请遵循以下实现准则：**

当对 **KeInsert *Xxx* DeviceQueue** 的调用返回 **FALSE** 时，调用方必须传递试图排队的 IRP，以便进一步处理其他驱动程序例程。
但是，对 **KeInsert *Xxx* DeviceQueue** 的调用会将设备队列对象的状态更改为 "忙碌"，因此将在队列中插入下一个 IRP，除非该驱动程序首先调用 **KeRemove *Xxx* DeviceQueue** 。

当设备队列对象的状态设置为 "忙碌" 时，驱动程序可以取消对 IRP 的排队以便进一步处理或通过调用以下支持例程之一将状态重置为 Not-Busy：

-   [**KeRemoveDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovedevicequeue) 删除队列头的 IRP

-   [**KeRemoveByKeyDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keremovebykeydevicequeue) 删除根据驱动程序确定的排序 *关键字* 值选择的 IRP

-   [**KeRemoveEntryDeviceQueue**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keremoveentrydevicequeue) 删除队列中的特定 irp，或确定特定 irp 是否在队列中

    **KeRemoveEntryDeviceQueue** 返回一个布尔值，指示 IRP 是否在设备队列中。

调用这些例程中的任何一项可从一个空但繁忙的设备队列中删除项，将队列状态更改为不忙。

每个设备队列对象均由内置执行单元旋转锁定保护 (不会在 [使用设备队列对象](#setting-up-and-using-device-queues) 图) 中显示。 因此，驱动程序可以将 Irp 插入到队列中，并通过在小于或等于 IRQL = 调度级别运行的任何驱动程序例程以多处理器安全的方式将其删除 \_ 。 由于此 IRQL 限制，驱动程序无法从其 ISR 或 [*SynchCritSection*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)例程（在 DIRQL 中运行）调用任何 **Ke *Xxx* DeviceQueue** 例程。

有关详细信息，请参阅 [管理硬件优先级](managing-hardware-priorities.md) 和 [旋转锁](./introduction-to-spin-locks.md) 。 有关特定支持例程的 IRQL 要求，请参阅例程的参考页。

 

