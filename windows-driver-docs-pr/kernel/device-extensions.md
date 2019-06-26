---
title: 设备扩展
description: 设备扩展
ms.assetid: 9ea59994-1112-4ae5-96a8-fa0670694b53
keywords:
- 设备对象 WDK 内核，设备扩展
- 设备扩展 WDK 内核
- 扩展 WDK 设备对象
- 更高级别的驱动程序扩展 WDK 内核
- 较低级别驱动程序扩展 WDK 内核
- 中间驱动程序扩展 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 230f5c3e2f96d3ef8ed0a5fd236a92fa365a0fe7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385016"
---
# <a name="device-extensions"></a>设备扩展





对于大多数中间和最低级别驱动程序设备扩展是一个设备对象与关联的最重要的数据结构。 其内部结构是驱动程序定义的并且它通常用于：

-   维护设备状态信息。

-   为任何内核定义的对象或其他系统资源，例如自旋锁，驱动程序使用提供存储。

-   保存任何数据驱动程序必须具有常驻和系统空间来执行其 I/O 操作中。

由于大多数总线、 函数和筛选器驱动程序 （最低级别和中间驱动程序） 执行在任意线程上下文中 （该的任何线程正好为最新），设备扩展是每个驱动程序的主位置维护设备状态和所有其他需要特定于设备的数据驱动程序。 例如，任何驱动程序，它实现[ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)或[ *CustomDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)例程通常提供所需的存储内核定义计时器和/或 DPC 设备扩展中的对象。

具有 ISR 每个驱动程序必须提供存储指向一组内核定义中断对象的指针，并且大多数设备驱动程序将此指针存储在设备扩展。 它创建一个设备对象，和每个驱动程序定义的内容和其自己的设备扩展的结构时，每个驱动程序确定设备扩展的大小。

I/O 管理器[ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)并[ **IoCreateDeviceSecure** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)例程分配内存的设备对象和扩展从非分页的内存池。

每个接收 IRP 的标准驱动程序例程还会收到指向表示请求的 I/O 操作的目标设备的设备对象的指针。 这些驱动程序例程可以通过此指针访问相应的设备扩展。 通常情况下， *DeviceObject*指针也是最低级别驱动程序的 ISR.的输入的参数

下图显示了一组代表驱动程序定义为设备扩展的最低级别驱动程序的设备对象的数据。 更高级别的驱动程序就无法为返回的一个中断对象指针提供存储[ **IoConnectInterrupt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterrupt) ，并传递给[ **KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)并[ **IoDisconnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodisconnectinterrupt)。 但是，更高级别的驱动程序将提供用于计时器和驱动程序是否在下图中显示的 DPC 对象存储*CustomTimerDpc*例程。 更高级别的驱动程序还可能会执行数值调节钮锁提供存储和联锁工作队列。

![说明的最低级别驱动程序的示例设备扩展的关系图](images/3devext.png)

除了提供用于中断对象指针的存储空间，最低级别的设备驱动程序必须提供中断自旋锁的存储其 ISR 处理的两个或多个设备上不同向量或是否有多个 ISR.中断 有关注册 ISR 的详细信息，请参阅[注册了 ISR](registering-an-isr.md)。

通常情况下，驱动程序存储指向其设备对象在其设备扩展中，如图所示。 驱动程序还可能在扩展中保留一份该设备的资源列表。

更高级别的驱动程序通常将指向下一步低驱动程序的设备对象的指针存储在其设备扩展。 更高级别的驱动程序必须将一个指针传递给下一个较低驱动程序的设备对象到[ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)之后它设置为 IRP 中的下一步低驱动程序的 I/O 堆栈位置中所述,[处理 Irp](handling-irps.md)。

另请注意，将 Irp 为较低级别的驱动程序分配任何更高级别的驱动程序必须指定新的 Irp 应具有多少个堆栈位置。 具体而言，如果更高级别的驱动程序调用[ **IoMakeAssociatedIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iomakeassociatedirp)， [ **IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)，或[ **IoInitializeIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinitializeirp)，它必须访问的目标设备对象的下一步低级驱动程序读取其**StackSize**值，以提供正确*StackSize*作为这些自变量支持例程。

更高级别的驱动程序可以通过返回的指针的下一步低级驱动程序的设备对象中读取数据时[ **IoAttachDeviceToDeviceStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack)，这样的驱动程序必须遵循这些实现准则：

-   永远不会尝试将数据写入到较低的驱动程序的设备对象。

    此原则的唯一例外是文件系统设置和清除 DO\_验证\_中的卷**标志**的较低级别可移动媒体驱动程序的设备对象。

-   永远不会尝试访问较低的驱动程序的设备扩展原因如下：

    -   没有安全方法对两个驱动程序之间的单个设备扩展访问进行同步。
    -   实现这种后门通信方案的驱动程序的一对无法单独升级、 不能有插入它们而无需更改现有的驱动程序源之间的中间驱动程序并不能进行重新编译并轻松地从一个 Windows 移动到下一个平台。

若要保留到下一个较低级别从一个 Windows 平台或版本的驱动程序及其互操作性，更高级别的驱动程序必须重复使用向用户提供了 Irp 或必须创建新的 Irp，并且它们必须使用[ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)通信对较低级别的驱动程序的请求。

 

 




