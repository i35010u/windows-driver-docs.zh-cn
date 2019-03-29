---
title: 为基于数据包的 DMA 分配适配器通道
description: 为基于数据包的 DMA 分配适配器通道
ms.assetid: c95e4b2d-ce19-453a-bcc5-4bb37fc5d9ed
keywords:
- DMA WDK 内核，基于数据包的系统
- 基于数据包的 DMA WDK 内核
- DMA 传输 WDK 内核，基于数据包的
- 分配适配器通道
- 适配器通道分配 WDK 内核
- AllocateAdapterChannel
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56986dd49aa3293cefa8c4774ad9cb0d28b2a2b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561914"
---
# <a name="allocating-an-adapter-channel-for-packet-based-dma"></a>为基于数据包的 DMA 分配适配器通道





若要准备基于数据包的系统 DMA，驱动程序调用[ **KeFlushIoBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff552041)并[ **AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)收到后[ **IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff550794)或者[ **IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff550819)请求。

该驱动程序调用这些例程之前, 其[ *DispatchRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)或[ *DispatchWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程 (或任何其他调度例程，处理 DMA 传输） 应已选中 IRP 的参数的有效性。 调度例程可能会让排队等待到另一个驱动程序例程进行进一步处理 IRP。

调用的驱动程序例程**AllocateAdapterChannel**必须执行在 IRQL = 调度\_级别。 以及指向返回的适配器对象的指针[ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)，它将调用时，驱动程序必须提供以下**AllocateAdapterChannel**:

-   指向目标设备对象的指针

-   入口点及其[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)例程

-   指向任何驱动程序确定上下文信息的指针*AdapterControl*例程将使用

**AllocateAdapterChannel**队列的驱动程序*AdapterControl*例程，运行时系统 DMA 控制器分配给此驱动程序和一系列[映射寄存器](map-registers.md)已分配有关驱动程序的 DMA 操作。

在进入时， *AdapterControl*例程接收*DeviceObject*并*上下文*指针传递到调用中**AllocateAdapterChannel**，以及一个句柄 (*MapRegisterBase*) 的分配的映射注册。

*AdapterControl*例程还会收到一个指向**DeviceObject-&gt;CurrentIrp**如果该驱动程序有[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程。 如果该驱动程序管理其自己的 Irp 队列 (而不是让*StartIo*例程)，该驱动程序应调用时传递的上下文的一部分包括指向当前 IRP 的**AllocateAdapterChannel**.

*AdapterControl*例程通常执行以下操作：

1.  将保存或初始化该驱动程序会维护有关 DMA 操作任何上下文。 上下文可能包括输入*MapRegisterBase*句柄驱动程序必须将传递给[ **MapTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff554402)并[ **FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917) ，并且可能**长度**从其 I/O 请求的传输堆栈中的位置。

2.  调用[ **MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539)跟**MapTransfer**。 请参阅[为基于数据包的 DMA 设置系统 DMA 控制器](setting-up-the-system-dma-controller-for-packet-based-dma.md)。

3.  将从属的设备设置开始在传输操作。

4.  返回的值**KeepObject**。

每个*AdapterControl*例程必须返回类型的系统定义的值[ **IO\_分配\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff550534)。 有关使用系统 DMA，驱动程序*AdapterControl*例程必须返回值**KeepObject**。 这将允许驱动程序保留系统 DMA 控制器的"所有权"，并分配的映射寄存器，直到它已转移所有请求的数据。

因为*AdapterControl*例程不能等待从属设备执行 DMA 的操作，每个*AdapterControl*例程必须在最低限度上，执行以下操作：

1.  保存上下文信息，请特别*MapRegisterBase*句柄，驱动程序的设备扩展、 控制器扩展或其他驱动程序可访问驻留的存储区域 （非分页缓冲池分配驱动程序） 中。

2.  返回**KeepObject**。

有关其他信息，请参阅[写入 AdapterControl 例程](writing-adaptercontrol-routines.md)。

另一个驱动程序例程 (可能[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)例程) 必须调用[ **FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917)时每个 DMA 传输操作已完成。 此例程还必须调用**MapTransfer**并**FlushAdapterBuffers**再次是否必须设置 DMA 控制器不止一次以满足当前 IRP 的传输请求。

当驱动程序已满足当前 IRP 的请求时，它必须调用[ **FreeAdapterChannel**](https://msdn.microsoft.com/library/windows/hardware/ff546507)。 应为最后一次调用后立即调用此支持例程**FlushAdapterBuffers**为当前的 IRP，以便系统 DMA 控制器可供使用 （通过任何驱动程序） 用于满足其他传输请求能迅速。

从属散播-聚集功能与设备的驱动程序还会返回**KeepObject**从其*AdapterControl*例程。 设备必须能够等待系统 DMA 控制器囿 DMA 操作时，驱动程序必须拆分给定的 DMA 请求之间。 在某些 Windows 平台上，此类设备可以传输最多的每个 DMA 操作的数据页因为 HAL 可以将单个映射寄存器分配给该设备的驱动程序。

 

 




