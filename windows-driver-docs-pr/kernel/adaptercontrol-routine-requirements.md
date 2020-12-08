---
title: AdapterControl 例程要求
description: AdapterControl 例程要求
keywords:
- AdapterControl 例程，要求
- AdapterControl 例程，编写
- 适配器对象 WDK 内核，编写 AdapterControl 例程
- DMA 传输 WDK 内核，编写 AdapterControl 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e16fccf330d418fba5a07febddcd58723f927182
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817181"
---
# <a name="adaptercontrol-routine-requirements"></a>AdapterControl 例程要求





[*AdapterControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)例程至少必须执行以下操作：

1.  保存输入 *MapRegisterBase* 值以及驱动程序为当前 IRP 执行一个或多个 DMA 传输操作所需的任何其他上下文信息。 每个 DMA 传输操作完成时，驱动程序必须将 *MapRegisterBase* 值传递到 [**FlushAdapterBuffers**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pflush_adapter_buffers) 。

2.  返回相应的 [**IO \_ 分配 \_ 操作**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_io_allocation_action) 值：

    -   **KeepObject** 如果设备是从属设备，以便驱动程序使用系统 DMA。

    -   **DeallocateObjectKeepRegisters** 如果设备为总线主机，则驱动程序使用基于数据包的总线主机 DMA。

根据驱动程序的设计，其 *AdapterControl* 例程还可以在返回 control 之前执行以下操作：

1.  确定传输在其设备上的起始位置。

2.  如果传输的起始位置导致其设备有任何限制，则计算可能的传输大小。

    通常情况下，调用 [**AllocateAdapterChannel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel) 的例程负责确定是否必须将传输请求拆分为部分传输，因为对每个 DMA 传输操作可用的 *NumberOfMapRegisters* 有任何特定于平台的限制，如前一部分中所述以及 [拆分传输请求](splitting-dma-transfer-requests.md)中的详细信息。

3.  设置与设备 (或控制器) 扩展中的每个传输请求有关的任何驱动程序维护状态。

    例如， *AdapterControl* 例程可能会调用 [**KeSetTimer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimer) ，其中包含用于驱动程序 DMA 传输操作的 [*CustomTimerDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983) 例程的入口点。

4.  使用 **&gt; MdlAddress** 上传递的 MDL 指针调用 [**MmGetMdlVirtualAddress**](./mm-bad-pointer.md) ，以获取传输开始的索引，适用于传递到 [**MapTransfer**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)。

5.  调用 **MapTransfer** 来设置系统 DMA 控制器或获取总线-主设备的物理到逻辑地址映射。

6.  使用通过调用 [**KeSynchronizeExecution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)调用的 [*SynchCritSection*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)例程对驱动程序的设备进行传输操作。 有关详细信息，请参阅 [使用关键部分](using-critical-sections.md)。

如果传输请求要求驱动程序执行部分传输操作序列以满足当前 IRP，则驱动程序的 [*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine) 或 [*CustomDpc*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine) 例程通常负责 reprogramming 设备，以便执行后续传输操作。 对于每个传入传输 IRP，只调用一次 *AdapterControl* 例程。

完成当前传输 IRP 的驱动程序例程（通常是 *DpcForIsr* 或 *CustomDpc* 例程）还负责通过分别调用 [**FreeAdapterChannel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel) 或 [**FreeMapRegisters**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers)来释放系统 DMA 控制器或主线主机适配器。 当完成其上一次部分传输操作，使从属 DMA 设备的驱动程序可以分配系统 DMA 控制器或主线主机驱动程序可以立即开始处理下一个传输 IRP 时，此驱动程序例程应尽快进行适当的调用。

 

