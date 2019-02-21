---
title: 拆分 DMA 传输请求
description: 拆分 DMA 传输请求
ms.assetid: 7d5b1649-1021-4876-a9c0-e6b156785ef2
keywords:
- I/O WDK 内核，拆分传输请求
- 拆分传输请求
- 转移请求拆分 WDK 内核
- 数据传输 WDK 内核，拆分请求
- 传输数据 WDK 内核拆分请求
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a90e32d18165df873a993c0e905f73a301af0b31
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525228"
---
# <a name="splitting-dma-transfer-requests"></a>拆分 DMA 传输请求





任何驱动程序可能需要拆分传输请求和执行多个 DMA 传输操作，以满足给定的 IRP，具体取决于以下：

-   数[映射寄存器](map-registers.md)返回的[ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)

-   中包含的数据要传输的字节**长度**IRP 的驱动程序的 I/O 堆栈位置的成员

-   页边界，在系统物理内存中，其中或从中驱动程序是将数据传输的缓冲区数

-   特定于设备的驱动程序的 DMA 操作的约束。 例如，"AT"磁盘驱动程序的系统必须拆分由于磁盘控制器限制超过 256 个扇区的传输请求。

驱动程序可以确定的传输指定的 IRP，如下所示的所有数据所需的映射寄存器的数量：

1.  调用[ **MmGetMdlVirtualAddress**](https://msdn.microsoft.com/library/windows/hardware/ff554539)，将指针传递到在 MDL **Irp-&gt;MdlAddress**，以获取缓冲区的起始虚拟地址。 请注意，驱动程序不能尝试访问使用此虚拟地址的内存。 返回的值**MmGetMdlVirtualAddress**的索引为 MDL，不一定是有效的地址。

2.  将返回的索引和的值传递**长度**中的驱动程序的 I/O 堆栈位置到 IRP [**地址\_AND\_大小\_TO\_跨度\_PAGES** ](https://msdn.microsoft.com/library/windows/hardware/ff540562)宏。

如果返回的值**地址\_AND\_大小\_TO\_跨度\_页**大于*NumberOfMapRegisters*值返回的**IoGetDmaAdapter**，驱动程序不能在单个操作中 DMA 此 IRP 的传输所有请求的数据。 相反，必须执行以下操作：

1.  拆分成大小将调整为适合可用映射寄存器 （和任何特定于设备的 DMA 约束） 的数量的部分缓冲区。

2.  执行所需满足的传输请求的多个 DMA 操作。

例如，假设**地址\_AND\_大小\_TO\_跨度\_页**指示十二个映射注册所需满足的传输请求，但*NumberOfMapRegisters*返回值**IoGetDmaAdapter**为仅 5。 （假定任何特定于设备的 DMA 约束）。在这种情况下，该驱动程序必须执行三个 DMA 传输操作，调用[ **MapTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff554402)三次以传输请求的 IRP 的所有数据。

系统的 DMA 的设备驱动程序使用各种技术来拆分 DMA 传输时没有足够的映射寄存器来满足使用单个 I/O 操作 IRP。 若要使用的一种方法是：

1.  调用[ **IoAllocateMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff548263)分配 MDL 描述用户缓冲区的一部分。

2.  调用[ **MmProbeAndLockPages** ](https://msdn.microsoft.com/library/windows/hardware/ff554664)锁定用户缓冲区的该部分。

3.  传输的数据缓冲区的该部分。

4.  调用[ **MmUnlockPages** ](https://msdn.microsoft.com/library/windows/hardware/ff556381)并执行以下任一操作：
    -   如果 MDL 驱动程序分配给在步骤 1 中的下一个传输足够大，则调用[ **MmPrepareMdlForReuse** ](https://msdn.microsoft.com/library/windows/hardware/ff554660)和重复步骤 2 至 4。
    -   否则，调用[ **IoFreeMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff549126)并重复步骤 1 至 4。

5.  调用[ **MmUnlockPages** ](https://msdn.microsoft.com/library/windows/hardware/ff556381)并[ **IoFreeMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff549126)的所有数据都传输时间。

最高级别的驱动程序不能锁定具有的整个用户缓冲区[ **MmProbeAndLockPages** ](https://msdn.microsoft.com/library/windows/hardware/ff554664)中具有有限的内存的计算机，它可以执行以下操作：

1.  调用[ **IoBuildSynchronousFsdRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548330)分配部分传输的 IRP 和锁定用户缓冲区的一部分。 锁定的区域通常是的倍数**页上\_大小**或调整大小以适应基础设备的传输能力。

2.  调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)个部分传输 IRP，以及调用[ **KeWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)等待一个事件对象驱动程序设置为与其部分传输 IRP，如果低级驱动程序返回状态\_PENDING。

3.  当它重新获得控制，请重复执行步骤 1 和 2，直至将所有数据传输，然后，完成原始 IRP。

存储类驱动程序将拆分为基础的 SCSI 端口/微型端口驱动程序的大型传输请求，它会分配其他 IRP 的传输请求的每一段。 它会注册[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)为每个驱动程序分配 IRP，跟踪完整传输请求的状态，并以释放驱动程序分配 Irp 例程。 然后它将发送这些 Irp 到端口驱动程序使用[ **IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)。

其他类/端口驱动程序可以使用此技术，仅当在类驱动程序可以确定多少映射到端口驱动程序可用的寄存器。 端口驱动程序必须将此配置信息存储在配对的类驱动程序注册表或配对的驱动程序必须定义专用接口，使用内部设备 I/O 控制请求，将传递数量的配置信息可用的映射从端口驱动程序注册到的类驱动程序。

DMA 设备的整体化驱动程序 （即，驱动程序不是类/端口对的一部分） 中，必须拆分为其自身的大型传输请求。 此类驱动程序通常拆分成部分的大型请求和执行一系列的 DMA 操作才能符合 IRP 的要求。

如果传输请求太大，基础设备驱动程序来处理，更高级别的驱动程序可以调用[ **MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539)并[ **IoBuildPartialMdl**](https://msdn.microsoft.com/library/windows/hardware/ff548324)，然后将设置为基础的设备驱动程序部分传输 Irp 的序列。

 

 




