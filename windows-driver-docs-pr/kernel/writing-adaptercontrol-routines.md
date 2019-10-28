---
title: 编写 AdapterControl 例程
description: 编写 AdapterControl 例程
ms.assetid: a5a7501f-ba4f-441e-be07-6a1b7fac9938
keywords:
- AdapterControl 例程，编写
- 适配器对象 WDK 内核，编写 AdapterControl 例程
- DMA 传输 WDK 内核，编写 AdapterControl 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3688e523d7dae131bce16fda26a0cd5c6f92c5d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835598"
---
# <a name="writing-adaptercontrol-routines"></a>编写 AdapterControl 例程





DMA 设备的大多数驱动程序都有一个[*AdapterControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)例程，该例程负责启动 DMA 操作。 （不需要*AdapterControl*例程的驱动程序包括那些[使用散播/聚集 dma](using-scatter-gather-dma.md)的驱动程序，以及[使用常见缓冲区、总线主 dma](using-common-buffer-bus-master-dma.md)的驱动程序。）

当驱动程序调用[**AllocateAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)时，如果系统 dma 控制器或总线主适配器可用于 DMA 操作，并且有足够的映射寄存器可用，则其*AdapterControl*例程将立即运行。 否则， *AdapterControl*例程将排队等候，直到这些资源可用。

如果驱动程序的*AdapterControl*例程返回**KeepObject**或**DEALLOCATEOBJECTKEEPREGISTERS** （从而保留系统 DMA 控制器通道或用于其他传输操作的总线主适配器），则驱动程序的[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)或[*CustomDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)例程负责在 DPC 例程完成当前 IRP 并返回控制权之前，通过调用[**FreeAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)或[**FreeMapRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers)来释放适配器对象或映射寄存器。

 

 




