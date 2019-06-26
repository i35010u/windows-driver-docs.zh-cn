---
title: 编写 AdapterControl 例程
description: 编写 AdapterControl 例程
ms.assetid: a5a7501f-ba4f-441e-be07-6a1b7fac9938
keywords:
- AdapterControl 例程编写
- 适配器对象 WDK 内核，编写 AdapterControl 例程
- DMA 传输 WDK 内核，编写 AdapterControl 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2086aefeb60e8d10f2063b0886ed5c2a8950e6b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374143"
---
# <a name="writing-adaptercontrol-routines"></a>编写 AdapterControl 例程





DMA 的设备的大多数驱动程序有[ *AdapterControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_control)例程，它负责启动 DMA 操作。 (不需要的驱动程序*AdapterControl*例程包括的[使用散播-聚集 DMA](using-scatter-gather-dma.md)它们的[使用常见缓冲区、 总线 master DMA](using-common-buffer-bus-master-dma.md)。)

当驱动程序调用[ **AllocateAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pallocate_adapter_channel)，将其*AdapterControl*如果系统 DMA 控制器或主机总线适配器可用于立即运行例程DMA 操作，如果不够映射寄存器和都可用。 否则为*AdapterControl*例程会排队，直到这些资源都可用。

如果驱动程序的*AdapterControl*例程返回**KeepObject**或**DeallocateObjectKeepRegisters** (因此保留系统 DMA 控制器通道或主总线适配器的其他传输操作），驱动程序的[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)或[ *CustomDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)例程负责释放适配器对象或映射通过调用注册[ **FreeAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_adapter_channel)或[ **FreeMapRegisters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_map_registers) DPC 之前例程完成当前的 IRP，并返回控件。

 

 




