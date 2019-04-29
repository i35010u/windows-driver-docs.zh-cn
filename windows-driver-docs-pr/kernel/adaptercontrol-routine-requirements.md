---
title: AdapterControl 例程要求
description: AdapterControl 例程要求
ms.assetid: 09ce4ad8-eb1b-4fd0-9a22-4249d09584b3
keywords:
- AdapterControl 例程要求
- AdapterControl 例程编写
- 适配器对象 WDK 内核，编写 AdapterControl 例程
- DMA 传输 WDK 内核，编写 AdapterControl 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 317f38427cf05454e11c3a2553399d4d2cfc5ad6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365858"
---
# <a name="adaptercontrol-routine-requirements"></a>AdapterControl 例程要求





最低限度[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)例程必须执行以下操作：

1.  将输入保存*MapRegisterBase*值以及该驱动程序必须执行一个或多个 DMA 传输操作的当前 IRP 的任何其他上下文信息。 该驱动程序必须通过*MapRegisterBase*值设置为[ **FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917) DMA 传输的每个操作何时完成。

2.  返回适当[ **IO\_分配\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff550534)值：

    -   **KeepObject**如果设备是从属的设备，因此驱动程序将使用系统 DMA。

    -   **DeallocateObjectKeepRegisters**设备是否总线 master，因此驱动程序使用基于数据包的、 总线 master DMA。

具体取决于驱动程序的设计，其*AdapterControl*例程还可以执行以下操作之前会将控件返回：

1.  确定在其设备上传输的起始位置。

2.  计算有可能，传输的大小因传输的起始位置提供其设备的任何限制。

    一般情况下，它负责调用的例程[ **AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)以确定是否传输请求必须拆分为分部由于任何特定于平台的传输限制*NumberOfMapRegisters*适用于每个 DMA 传输操作，如在上一部分中所述和中详细介绍[拆分传输请求](splitting-dma-transfer-requests.md)。

3.  设置每个传输中的设备 （或控制器） 请求扩展有关的任何驱动程序维护状态。

    例如， *AdapterControl*可能会在调用例程[ **KeSetTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff553286)的入口点与[ *CustomTimerDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)超时时 DMA 的驱动程序的传输操作的例程。

4.  调用[ **MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539) MDL 指针在传递**Irp-&gt;MdlAddress**为获取的传输，适合传递开始的索引向[ **MapTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff554402)。

5.  调用**MapTransfer**设置系统 DMA 控制器或获取总线母版设备的物理到逻辑地址映射。

6.  通过使用程序适用于传输操作中，驱动程序的设备[ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)调用调用的例程[ **KeSynchronizeExecution**](https://msdn.microsoft.com/library/windows/hardware/ff553302). 有关详细信息，请参阅[使用临界区](using-critical-sections.md)。

如果传输请求需要驱动程序执行部分传输操作，以满足当前 IRP，驱动程序的一系列[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)或[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)例程是通常负责重新编程的后续传输操作设备。 *AdapterControl*例程只调用一次每个传入传输 IRP。

完成当前传输 IRP，通常的驱动程序例程*DpcForIsr*或*CustomDpc*例程，也会释放系统 DMA 控制器或主机总线适配器通过调用[ **FreeAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff546507)或[ **FreeMapRegisters**](https://msdn.microsoft.com/library/windows/hardware/ff546513)分别。 此驱动程序例程应完成其最后一个部分传输操作后，以便驱动程序的从属 DMA 设备可以分配系统 DMA 控制器或主总线驱动程序可以开始处理下一个传输尽可能快地进行适当的调用IRP 迅速。

 

 




