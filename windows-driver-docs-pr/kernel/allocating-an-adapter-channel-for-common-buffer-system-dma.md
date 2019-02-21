---
title: 为常见缓冲区系统 DMA 分配适配器通道
description: 为常见缓冲区系统 DMA 分配适配器通道
ms.assetid: 3b426b5e-e555-458c-8e16-0d59a7cb9bd6
keywords:
- 分配适配器通道
- 适配器通道分配 WDK 内核
- AllocateAdapterChannel
- 系统 DMA WDK 内核，常见的缓冲区
- 常见缓冲区 DMA WDK 内核
- DMA 传输 WDK 内核，常见的缓冲区
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5efb04bf7a49f1c2b10e02069f860222b491bd43
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524581"
---
# <a name="allocating-an-adapter-channel-for-common-buffer-system-dma"></a>为常见缓冲区系统 DMA 分配适配器通道





驱动程序调用[ **AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)后其[ *DispatchRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)或[ *DispatchWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程 （或任何其他处理 DMA 传输的调度例程） 已选中 IRP 的参数的有效性，可能是排队到进行进一步处理，另一个驱动程序例程的一个或多个 Irp 并且可能是加载其与数据传输，如果相应的常见缓冲区。

调用的驱动程序例程**AllocateAdapterChannel**必须执行在 IRQL = 调度\_级别。 **AllocateAdapterChannel**例程队列的驱动程序[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)例程，运行后系统 DMA 控制器已分配给此驱动程序和一个设置的[映射寄存器](map-registers.md)已分配驱动程序的 DMA 操作。

在进入时， *AdapterControl*例程提供给设备对象和上下文调用中传递指针**AllocateAdapterChannel**，同时为分配的映射的句柄注册。 *AdapterControl*例程还提供一个指向**DeviceObject-&gt;CurrentIrp**如果该驱动程序有[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程。 如果该驱动程序管理的 Irp 自己队列，而不让*StartIo*例程，该驱动程序应包括一个指向当前 IRP 传递时，它调用的上下文数据的一部分**AllocateAdapterChannel**.

*AdapterControl*例程通常执行以下操作：

1.  将保存或初始化该驱动程序会维护有关 DMA 操作任何上下文。 上下文可能包括输入*MapRegisterBase*句柄驱动程序必须将传递给[ **MapTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff554402)并[ **FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917) ，并且可能**长度**从其 I/O 请求的传输堆栈中的位置。

2.  将从属的设备设置开始在传输操作。

3.  返回的值**KeepObject**。

有关其他信息，请参阅[写入 AdapterControl 例程](writing-adaptercontrol-routines.md)。

使用系统 DMA 控制器的自动初始化模式的驱动程序*AdapterControl*例程必须返回值**KeepObject**。 这将允许驱动程序保留系统 DMA 控制器的"所有权"，并分配映射 register(s)，直到它已传输的所有数据。

因为*AdapterControl*例程不能等待执行 DMA 的操作，从属设备*AdapterControl*例程至少必须执行以下操作：

1.  保存上下文信息，请特别*MapRegisterBase*句柄，驱动程序的设备扩展、 控制器扩展或其他驱动程序可访问驻留的存储区域 （非分页缓冲池分配驱动程序） 中。

2.  返回**KeepObject**。

另一个驱动程序例程 (可能[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)例程) 必须调用[ **FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917)和[ **FreeAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff546507) DMA 传输操作何时完成。

 

 




