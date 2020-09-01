---
title: 驱动程序管理的 IRP 队列
description: 驱动程序管理的 IRP 队列
ms.assetid: b701e4aa-96ba-44af-96a5-b6cecf075bac
keywords:
- 设备队列 WDK Irp，对象
- Irp WDK 内核，队列
- 队列 Irp
- 出列的 Irp
- 内部 IRP 队列 WDK 内核
- 取消安全 IRP 队列 WDK 内核
- 驱动程序管理的 IRP 队列 WDK 内核
- 补充 IRP 队列 WDK 内核
- 联锁 IRP 将 WDK 内核排队
- 设备队列 WDK Irp
- 设备队列 WDK Irp，关于设备队列
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 954cb7afa5bb7fdb3b0a82ee42eff21ceaf13f27
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185191"
---
# <a name="driver-managed-irp-queues"></a>驱动程序管理的 IRP 队列





除了文件系统驱动程序，i/o 管理器将 () 的设备队列对象与驱动程序创建的每个设备对象相关联。

大多数设备驱动程序调用 i/o 管理器的支持例程来使用关联的设备队列，只要目标设备对象的设备 i/o 请求速度快于驱动程序可将其处理完成，就会持有 Irp。 使用此方法时，Irp 会排入驱动程序提供的 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程。

为了获得良好的性能，大多数中间驱动程序会将 Irp 直接传递到较低的驱动程序，因此中间驱动程序几乎不会使用与其各自的设备对象关联的设备队列。

但是，可以通过显式设置一个或多个设备队列、互锁队列或取消安全队列来设计驱动程序来管理 Irp 的内部队列。 如果驱动程序控制与 i/o 操作重叠的设备，此方法特别有用。 对于这种设备，可能很难只使用单个队列为同一目标设备对象管理两个或更多个 Irp 的并发处理。

生成内部队列的最简单方法是使用 "取消安全 IRP 队列" 框架。 您可以在您的驱动程序中实现您选择的队列机制。 然后，你可以使用 [**IoCsqInitialize**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinitialize) 来注册一组回调例程，用于处理 IRP 插入和删除操作，以及锁定和解锁队列。 取消安全 IRP 队列框架提供了 [**IoCsqInsertIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirp)、 [**IoCsqRemoveIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremoveirp)和 [**IoCsqRemoveNextIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqremovenextirp) 例程，这些例程自动使用回调例程从驱动程序的队列中安全地插入和删除 irp。 系统还使用回调例程安全删除任何已取消的 Irp。

你还可以选择在设备控制器的驱动程序中为 Irp 设置补充队列，以用于一组异类物理设备。 例如，SCSI 端口驱动程序将设备队列对象用于内部队列。 此驱动程序有一个 *StartIo* 例程，并将设备队列对象设置为补充队列，并将设备队列添加到其创建的设备对象，以代表 HBA。 SCSI 端口驱动程序使用其补充设备队列来保存绑定到 HBA 控制的 SCSI 总线上的特定逻辑单元的 Irp (es) 。

系统软盘控制器驱动程序是没有 *StartIo* 例程并使用联锁队列的驱动程序的一个示例。 此驱动程序将设置一个双向链接的互锁队列，其中，驱动程序及其设备专用线程将在其中插入和删除 Irp。

内核定义设备队列对象类型。 执行组件支持组件提供用于在联锁队列中插入和删除 Irp 的例程。 适用于 Windows XP 和更高版本 Windows 的驱动程序可以使用 [取消安全 IRP 队列](cancel-safe-irp-queues.md) 来处理 IRP 队列。

以下部分介绍如何使用设备队列、互锁队列和取消安全队列：

[设置和使用设备队列](setting-up-and-using-device-queues.md)

[管理设备队列](managing-device-queues.md)

[设置和使用联锁队列](setting-up-and-using-interlocked-queues.md)

[使用驱动程序创建的线程管理联锁队列](managing-interlocked-queues-with-a-driver-created-thread.md)

[可安全取消的 IRP 队列](cancel-safe-irp-queues.md)

 

