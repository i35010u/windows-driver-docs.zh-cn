---
title: 设备扩展
description: 设备扩展
ms.assetid: 9ea59994-1112-4ae5-96a8-fa0670694b53
keywords:
- 设备对象 WDK 内核，设备扩展
- 设备扩展 WDK 内核
- 扩展 WDK 设备对象
- 高级驱动程序扩展 WDK 内核
- 低级驱动程序扩展 WDK 内核
- 中间驱动程序扩展 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9653802367f371f9ff814f0a2949f4e891529799
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191927"
---
# <a name="device-extensions"></a>设备扩展





对于大多数中间和最低级别的驱动程序，设备扩展是与设备对象相关的最重要的数据结构。 它的内部结构是由驱动程序定义的，它通常用于：

-   维护设备状态信息。

-   为驱动程序使用的任何内核定义的对象或其他系统资源（如旋转锁）提供存储。

-   保存驱动程序必须驻留的任何数据，并保存在系统空间中以执行其 i/o 操作。

由于大多数总线、函数和筛选器驱动程序都 (最低级别和中间驱动程序) 在任意线程上下文中执行， (任何线程发生在当前) 的情况下，设备扩展就是用于维护设备状态的每个驱动程序的主要位置以及驱动程序所需的所有其他设备特定数据。 例如，任何实现 [*CustomTimerDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983) 或 [*CustomDpc*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine) 例程的驱动程序通常都会为设备扩展中所需的内核定义的计时器和/或 DPC 对象提供存储空间。

具有 ISR 的每个驱动程序都必须为指向一组内核定义中断对象的指针提供存储，并且大多数设备驱动程序将此指针存储在设备扩展中。 每个驱动程序在创建设备对象时确定设备扩展的大小，每个驱动程序定义其自己的设备扩展的内容和结构。

I/o 管理器的 [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice) 和 [**IoCreateDeviceSecure**](/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure) 例程为设备对象分配内存，并为非分页内存池分配扩展。

接收 IRP 的每个标准驱动程序例程还会接收指向设备对象的指针，该对象表示请求的 i/o 操作的目标设备。 这些驱动程序例程可以通过此指针访问相应的设备扩展。 通常， *DeviceObject* 指针也是最底层驱动程序 ISR 的输入参数。

下图显示了一组代表驱动程序定义的数据，适用于最底层驱动程序的设备对象的设备扩展。 较高级别的驱动程序不会为 [**IoConnectInterrupt**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt) 返回的中断对象指针提供存储，并将其传递给 [**KeSynchronizeExecution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution) 和 [**IoDisconnectInterrupt**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterrupt)。 但是，如果驱动程序具有 *CustomTimerDpc* 例程，则更高级别的驱动程序将为下图中所示的计时器和 DPC 对象提供存储空间。 较高级别的驱动程序还可以为执行人员旋转锁定和联锁工作队列提供存储。

![说明最低级别驱动程序的设备扩展示例的关系图](images/3devext.png)

除了为中断对象指针提供存储外，如果其 ISR 处理不同矢量上两个或更多设备的中断或者具有多个 ISR，则最低级别的设备驱动程序必须为中断旋转锁定提供存储。 有关注册 ISR 的详细信息，请参阅 [注册 isr](registering-an-isr.md)。

通常，驱动程序会在其设备扩展中存储指向其设备对象的指针，如图所示。 驱动程序还可以保留设备在扩展中的资源列表的副本。

较高级别的驱动程序通常会在其设备扩展中存储一个指向下一个较低驱动程序的设备对象的指针。 更高级别的驱动程序必须将指向下一个较低驱动程序的设备对象的指针传递到 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)，然后再在 irp 中设置下一个较低版本的驱动程序的 i/o 堆栈位置（如 [处理 irp](handling-irps.md)中所述）。

另请注意，为较低级别的驱动程序分配 Irp 的任何较高级别的驱动程序必须指定新的 Irp 应具有多少个堆栈位置。 特别是，如果较高级别的驱动程序调用 [**IoMakeAssociatedIrp**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iomakeassociatedirp)、 [**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)或 [**IoInitializeIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeirp)，则它必须访问下一级驱动程序的目标设备对象，以读取其 **StackSize** 值，以便提供正确的 *StackSize* 作为这些支持例程的参数。

虽然更高级别的驱动程序可以通过 [**IoAttachDeviceToDeviceStack**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)返回的指针从下一级驱动程序的设备对象中读取数据，但此类驱动程序必须遵循以下实现准则：

-   切勿尝试将数据写入驱动程序的设备对象。

    此准则的唯一例外是 "文件系统"，这些系统设置和 \_ 清除 \_ "在较低级别的可移动媒体驱动程序的设备对象 **标志** 中验证卷"。

-   由于以下原因，永远不要尝试访问该驱动程序的设备扩展：

    -   没有安全的方法可以同步对两个驱动程序之间的单个设备扩展的访问。
    -   一对实现此类后门通信方案的驱动程序不能单独升级，不能在不更改现有驱动程序源的情况下在它们之间插入中间驱动程序，并且不能轻松地从一个 Windows 平台重新编译并将其移动到下一平台。

若要保持与较低级别驱动程序的互操作性（从一个 Windows 平台或版本到下一个版本），更高级别的驱动程序必须重新使用其给定的 Irp，或者必须创建新的 Irp，并且它们必须使用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 将请求传递给较低级别的驱动程序。

 

