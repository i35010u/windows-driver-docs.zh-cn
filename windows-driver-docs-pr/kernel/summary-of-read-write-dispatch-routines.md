---
title: 读/写 Dispatch 例程摘要
description: 读/写 Dispatch 例程摘要
ms.assetid: 2ab1cde7-89e8-449f-b2a0-12aa0762ebf3
keywords:
- DispatchRead 例程
- DispatchWrite 例程
- DispatchReadWrite 例程
- 调度例程 WDK 内核，DispatchReadWrite 例程
- 调度例程 WDK 内核，DispatchWrite 例程
- 调度例程 WDK 内核，DispatchRead 例程
- 读/写调度例程 WDK 内核
- IRP_MJ_WRITE I/O 函数代码
- IRP_MJ_READ I/O 函数代码
- 数据传输 WDK 内核，读/写调度例程
- 传输数据 WDK 内核，读/写调度例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50967db82177f76da45908b461d4701f2b646eb6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331932"
---
# <a name="summary-of-readwrite-dispatch-routines"></a>读/写 Dispatch 例程摘要





在实现时记住以下几点[ *DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)， [ *DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)，或[ *DispatchReadWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程：

-   它负责的分层驱动程序来检查传入读/写 Irp 的有效性之前设置 IRP 中的下一步低级驱动程序的 I/O 堆栈位置参数，链中的最高级别的驱动程序。

-   通常，中间和最低级别的驱动程序可以依赖于将向下传输请求具有有效的参数传递其链中的最高级别的驱动程序。 但是，任何驱动程序可以在 IRP，其 I/O 堆栈位置执行完整性检查的参数和每个设备驱动程序应检查可能会违反其设备施加任何限制条件的参数。

-   如果*DispatchReadWrite*例程完成并出现错误 IRP，但它应设置 I/O 堆栈位置**状态**成员使用适当的 NTSTATUS 类型值，设置**信息**成员为零，并调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)与 IRP 和一个*PriorityBoost*的 IO\_否\_增量。

-   如果驱动程序将使用缓冲的 I/O，它可能需要定义包含要传输的数据的结构，并可能需要一定数量的这些结构在内部进行缓冲。

-   如果驱动程序使用直接 I/O，则可能需要检查是否在 MDL **Irp-&gt;MdlAddress**介绍基础设备来处理单个传输中包含过多的数据 （或过多的分页符） 的缓冲区操作。 如果是这样，该驱动程序必须拆分到一系列较小的传输操作的原始传输请求。

    紧密耦合的类驱动程序可能会拆分此类请求在其*DispatchReadWrite*例程其基础端口驱动程序。 SCSI 类驱动程序，尤其是对于大容量存储设备，需要执行此操作。 有关 SCSI 驱动程序要求的详细信息，请参阅[存储设备驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff566976)。

-   较低级别的设备驱动程序*DispatchReadWrite*例程应推迟将大型传输请求拆分为分部传输，直到另一个驱动程序例程取消排队 IRP，若要设置设备进行传输。

-   如果较低级别设备驱动程序队列以做进一步处理由其自己的例程的读/写 IRP，它必须调用[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)队列 IRP 之前。 *DispatchReadWrite*例程也必须返回具有状态控件\_PENDING 在这些情况下。

-   如果*DispatchReadWrite*例程将传递到较低的驱动程序 IRP，它必须设置 IRP 中的下一步低驱动程序的 I/O 堆栈位置。 是否更高级别的驱动程序还设置[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程中之前将其传递对与 IRP [ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)取决于设计的驱动程序和其下分层。

    但是，更高级别的驱动程序必须调用[ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)调用之前[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)前提是它分配任何资源，例如 Irp 或内存。 其*IoCompletion*例程必须释放所有驱动程序分配的资源，较低的驱动程序之前完成请求时*IoCompletion*例程调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)与原始 IRP。

-   如果更高级别的驱动程序将 Irp 为低级驱动程序可能包含基础的可移动介质设备驱动程序分配，分配驱动程序必须建立中它会分配每个 IRP 的线程上下文。

 

 




