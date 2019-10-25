---
title: 为公用缓冲区系统 DMA 分配适配器通道
description: 为公用缓冲区系统 DMA 分配适配器通道
ms.assetid: 3b426b5e-e555-458c-8e16-0d59a7cb9bd6
keywords:
- 分配适配器通道
- 适配器通道分配 WDK 内核
- AllocateAdapterChannel
- 系统 DMA WDK 内核，公共缓冲区
- 常见缓冲区 DMA WDK 内核
- DMA 传输 WDK 内核，公共缓冲区
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e03e0ba87c32a9998458fb7d0410575942b25ef1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828663"
---
# <a name="allocating-an-adapter-channel-for-common-buffer-system-dma"></a>为公用缓冲区系统 DMA 分配适配器通道





驱动程序在其[*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)或[*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程（或处理 DMA 传输的任何其他调度例程）后调用[**AllocateAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel) ，已检查 IRP 的参数的有效性，可能已将一个或多个 irp 排队到其他用于进一步处理的驱动程序例程，并且可能会加载其包含要传输的数据的通用缓冲区（如果适用）。

调用**AllocateAdapterChannel**的驱动程序例程必须以 IRQL = 调度\_级别执行。 **AllocateAdapterChannel**例程将排队驱动程序的[*AdapterControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)例程，该例程在系统 dma 控制器分配到此驱动程序之后运行，并为驱动程序的 DMA 操作分配了一组[映射寄存器](map-registers.md)。

进入时， *AdapterControl*例程提供指向设备对象的指针，并向**AllocateAdapterChannel**调用传递的上下文，以及分配的映射寄存器的句柄。 如果驱动程序有[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程， *AdapterControl*例程还会获得一个指向**DeviceObject&gt;CurrentIrp**的指针。 如果驱动程序管理自己的 Irp 队列，而不是使用*StartIo*例程，则驱动程序应在调用**AllocateAdapterChannel**时，在它传递的上下文数据中包含指向当前 IRP 的指针。

*AdapterControl*例程通常执行以下操作：

1.  保存或初始化驱动程序维护的任何有关 DMA 操作的上下文。 上下文可能包括*MapRegisterBase*的输入，驱动程序必须将该句柄传递给[**MapTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)和[**FlushAdapterBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers) ，还可能包括从 IRP 中的 I/o 堆栈位置请求的传输**长度**。

2.  设置从属设备以启动传输操作。

3.  返回值**KeepObject**。

有关其他信息，请参阅[编写 AdapterControl 例程](writing-adaptercontrol-routines.md)。

对于使用系统 DMA 控制器的自动初始化模式的驱动程序， *AdapterControl*例程必须返回值**KeepObject**。 这使得驱动程序能够保留系统 DMA 控制器的 "所有权" 和分配的映射寄存器，直到传输所有数据为止。

由于*AdapterControl*例程无法等待从属设备执行 DMA 操作，因此*AdapterControl*例程至少必须执行以下操作：

1.  保存上下文信息，尤其是驱动程序的设备扩展中的*MapRegisterBase*句柄、控制器扩展或驱动程序可访问的其他常驻存储区域（驱动程序分配的非分页池）。

2.  返回**KeepObject**。

DMA 传输操作完成后，另一个驱动程序例程（可能是[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)例程）必须调用[**FlushAdapterBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers)和[**FreeAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel) 。

 

 




