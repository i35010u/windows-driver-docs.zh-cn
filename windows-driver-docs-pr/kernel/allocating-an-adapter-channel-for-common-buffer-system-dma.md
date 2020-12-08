---
title: 为公用缓冲区系统 DMA 分配适配器通道
description: 为公用缓冲区系统 DMA 分配适配器通道
keywords:
- 分配适配器通道
- 适配器通道分配 WDK 内核
- AllocateAdapterChannel
- 系统 DMA WDK 内核，公共缓冲区
- 常见缓冲区 DMA WDK 内核
- DMA 传输 WDK 内核，公共缓冲区
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21f5967c501d171833720671ace5236e79ee0960
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836949"
---
# <a name="allocating-an-adapter-channel-for-common-buffer-system-dma"></a>为公用缓冲区系统 DMA 分配适配器通道





驱动程序在其 [*DispatchRead*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)或 [*DispatchWrite*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) (例程后调用 [**AllocateAdapterChannel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel) ，或者处理 DMA 传输的任何其他调度例程) 检查 IRP 的参数的有效性，可能将一个或多个 irp 排队给另一个驱动程序例程进行进一步处理，并可能会加载其包含要传输的数据的通用缓冲区（如果适用）。

调用 **AllocateAdapterChannel** 的驱动程序例程必须以 IRQL = 调度级别执行 \_ 。 **AllocateAdapterChannel** 例程将排队驱动程序的 [*AdapterControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)例程，该例程在系统 dma 控制器分配到此驱动程序之后运行，并为驱动程序的 DMA 操作分配了一组 [映射寄存器](map-registers.md)。

进入时， *AdapterControl* 例程提供指向设备对象的指针，并向 **AllocateAdapterChannel** 调用传递的上下文，以及分配的映射寄存器的句柄。 如果驱动程序有 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程，则还会向 *AdapterControl* 例程提供一个指向 **DeviceObject- &gt; CurrentIrp** 的指针。 如果驱动程序管理自己的 Irp 队列，而不是使用 *StartIo* 例程，则驱动程序应在调用 **AllocateAdapterChannel** 时，在它传递的上下文数据中包含指向当前 IRP 的指针。

*AdapterControl* 例程通常执行以下操作：

1.  保存或初始化驱动程序维护的任何有关 DMA 操作的上下文。 上下文可能包括 *MapRegisterBase* 的输入，驱动程序必须将该句柄传递给 [**MapTransfer**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer) 和 [**FlushAdapterBuffers**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers) ，还可能包括从 IRP 中的 I/o 堆栈位置请求的传输 **长度** 。

2.  设置从属设备以启动传输操作。

3.  返回值 **KeepObject**。

有关其他信息，请参阅 [编写 AdapterControl 例程](writing-adaptercontrol-routines.md)。

对于使用系统 DMA 控制器的自动初始化模式的驱动程序， *AdapterControl* 例程必须返回值 **KeepObject**。 这使得驱动程序能够保留系统 DMA 控制器的 "所有权"，并在) 传输所有数据之前，将 (中分配的映射寄存器。

由于 *AdapterControl* 例程无法等待从属设备执行 DMA 操作，因此 *AdapterControl* 例程至少必须执行以下操作：

1.  保存上下文信息，尤其是驱动程序的设备扩展中的 *MapRegisterBase* 句柄、控制器扩展或驱动程序可访问的其他可访问的常驻存储区域 (驱动程序) 分配的非分页池。

2.  返回 **KeepObject**。

另一个驱动程序例程 (可能是 [*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine) 例程) 必须在 DMA 传输操作完成后调用 [**FlushAdapterBuffers**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers) 和 [**FreeAdapterChannel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel) 。

 

