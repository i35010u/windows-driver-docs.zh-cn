---
title: 定义和使用事件对象
description: 定义和使用事件对象
ms.assetid: 4b7807f0-bbea-4402-b028-9ac73724717f
keywords:
- 事件对象 WDK 内核
- 等待事件对象
- 同步事件 WDK 内核
- 通知事件 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 186d9fc358ff298d74d54169a44baecee662c9db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828426"
---
# <a name="defining-and-using-an-event-object"></a>定义和使用事件对象





使用事件对象的任何驱动程序都必须先调用[**KeInitializeEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeevent)、 [**IoCreateNotificationEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatenotificationevent)或[**IoCreateSynchronizationEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesynchronizationevent) ，然后才能等待、设置、清除或重置该事件。 下图说明了具有线程的驱动程序如何使用事件对象进行同步。

![说明等待事件对象的关系图](images/3evntobj.png)

如上图所示，此类驱动程序必须为必须驻留的事件对象提供存储。 驱动程序可以使用驱动程序创建的设备对象的[设备扩展](device-extensions.md)，如果控制器扩展使用[控制器对象](using-controller-objects.md)或由驱动程序分配的非分页池，则可以使用控制器扩展。

当驱动程序调用**KeInitializeEvent**时，它必须将一个指针传递到该事件对象的驱动程序的常驻存储。 此外，调用方必须为事件对象指定初始状态（已发出信号或未收到信号）。 调用方还必须指定事件类型，该类型可以是以下类型之一：

-   **SynchronizationEvent**

    如果*同步事件*设置为 "已终止" 状态，则等待事件重置为 "无终止" 状态的单个线程将有资格执行执行，并且事件的状态将自动重置为 "未终止"。

    这种类型的事件有时称为*autoclearing 事件*，因为每次满足等待时，其信号状态将自动重置。

-   **NotificationEvent**

    如果*通知事件*设置为 "已终止" 状态，则等待事件重置为 "无终止" 状态的所有线程都有资格执行执行，事件仍处于 "已终止" 状态，直到出现显式重置为 "未终止" 的情况：即使用给定的*事件*指针调用了[**KeClearEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keclearevent)或[**KeResetEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keresetevent) 。

很少有设备或中间驱动程序具有单个驱动程序专用线程，只需等待一组线程，就可以通过等待保护共享资源的事件来同步其操作。

大多数使用事件对象等待 i/o 操作完成的驱动程序在调用**KeInitializeEvent**时，将输入*类型*设置为**NotificationEvent** 。 为使用[**IoBuildSynchronousFsdRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)或[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)创建的 irp 设置的事件对象几乎始终初始化为**NotificationEvent** ，因为调用方将等待的事件通知，其中一个或多个低级驱动程序已满足请求。

驱动程序自行初始化后，其驱动程序专用线程（如果有）和其他例程可以同步其对事件的操作。 例如，如果驱动程序的线程管理 Irp 的队列（如系统软盘控制器驱动程序），则可能会对事件同步 IRP 处理，如下图所示：

1.  线程在设备上取消了用于处理的 IRP，并使用指向已初始化事件对象的驱动程序提供的存储的指针调用[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) 。

2.  其他驱动程序例程会执行满足 IRP 所需的 i/o 操作，并在这些操作完成后，驱动程序的[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)例程使用指向事件对象的指针（驱动程序确定的优先级）调用[**KeSetEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent) 。增大线程的量（*增量*，如上图所示），并将布尔值*Wait*设置为**FALSE**。 调用**KeSetEvent**会将事件对象设置为终止状态，从而将等待线程的状态更改为 "就绪"。

3.  处理器可用时，内核会立即调度线程以执行：也就是说，具有较高优先级的其他线程目前处于 "就绪" 状态，并且没有要在更高的 IRQL 上运行的内核模式例程。

    如果*DpcForIsr*尚未将**IoCompleteRequest**与 IRP 一起调用，则该线程现在可以完成 irp，并可以将另一个 IRP 取消排队以便在设备上进行处理。

**如果**调用**KeSetEvent**并将*Wait*参数设置为 TRUE，则指示调用方在从 KeSetEvent 返回时立即调用[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)或[**KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)支持例程.

**请考虑以下设置***Wait***参数 toKeSetEvent 的准则：**

以 IRQL &lt; 调度\_级别运行的可分页的线程或可分页的驱动程序例程不应调用**KeSetEvent** ，并将*Wait*参数设置为**TRUE**。 如果调用方在对**KeSetEvent**和**KeWaitForSingleObject**或**KeWaitForMultipleObjects**的调用之间分页，则此类调用将导致严重的页错误。

任何以 IRQL = 调度\_级别运行的标准驱动程序例程都不会在不关闭系统的情况下等待任何调度程序对象上的非零间隔。 但是，此类例程可以在小于或等于调度\_级别的 IRQL 时调用**KeSetEvent** 。

有关标准驱动程序例程运行的 IRQLs 的摘要，请参阅[管理硬件优先级](managing-hardware-priorities.md)。

**KeResetEvent**返回给定*事件*以前的状态：是否将其设置为 "已终止" 或 "在调用**KeResetEvent**时未设置"。 **KeClearEvent**只需将给定*事件*的状态设置为 "无-已终止"。

**对于何时调用上述支持例程，请考虑以下准则：**

为了获得更好的性能，每个驱动程序都应调用**KeClearEvent** ，除非调用方需要**KeResetEvent**返回的信息来确定接下来要执行的操作。

 

 




