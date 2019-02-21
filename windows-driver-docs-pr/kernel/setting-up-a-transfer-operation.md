---
title: 设置传输操作中
description: 设置传输操作中
ms.assetid: cabac16d-b946-4b96-af2c-5fd0a0d848da
keywords:
- 主总线 DMA WDK 内核
- DMA 传输 WDK 内核，总线 master DMA
- 适配器对象 WDK 内核，总线 master DMA
- 逻辑地址范围 WDK DMA
- 地址 WDK DMA
- 将操作 WDK DMA 转移
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbeb0007d2c637a21dd0968f9d4c8c880fb86e96
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541630"
---
# <a name="setting-up-a-transfer-operation"></a>设置传输操作中





当[ **AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)将控制转移到的驱动程序[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)例程，它已经分配了一组映射注册。 但是，该驱动程序必须映射系统物理内存的当前 IRP 的传输请求到主机总线适配器的逻辑地址范围，如下所示：

1.  调用[ **MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539)与在 MDL **Irp-&gt;MdlAddress**若要获取系统的物理地址传输应在何处开始索引。

    返回值是必需的参数 (*CurrentVa*) 到[ **MapTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff554402)。

2.  调用**MapTransfer**以将 IRP 的缓冲区的系统的物理地址范围映射到主机总线适配器的逻辑地址范围。

然后，驱动程序可以将设置用于在传输操作的适配器。 下图显示所涉及步骤中设置传输。

![演示如何设置传输操作中的关系图](images/3dmabus.png)

上一图所示，驱动程序的*AdapterControl*例程设置总线 master DMA 操作，如下所示：

1.  *AdapterControl*例程获取开始传输地址。 将满足 IRP，所需的初始传输*AdapterControl*例程调用[ **MmGetMdlVirtualAddress**](https://msdn.microsoft.com/library/windows/hardware/ff554539)，将指针传递到在 MDL **Irp-&gt;MdlAddress**，这对于此 DMA 传输描述缓冲区。

    **MmGetMdlVirtualAddress**返回驱动程序可用作索引的系统的物理地址传输应开始的位置的虚拟地址。

    如果 IRP 需要多个传输操作，该驱动程序将计算的已更新的起始地址，如在本部分后面所述。

2.  *AdapterControl*例程将返回的地址保存**MmGetMdlVirtualAddress**或在步骤 1 中计算。 此地址是必需的参数 (*CurrentVa*) 到[ **MapTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff554402)。

3.  *AdapterControl*例程调用**MapTransfer**，这会返回该驱动程序可以从该处编程主机总线适配器若要开始在传输操作的逻辑地址。 在调用**MapTransfer**，驱动程序提供以下参数：
    -   所返回的适配器对象指针[ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)

    -   指向在 MDL **Irp-&gt;MdlAddress**为当前的 IRP

    -   *MapRegisterBase*句柄传递给驱动程序的*AdapterControl*例程由**AllocateAdapterChannel** (请参阅[分配总线 Master适配器对象](allocating-the-bus-master-adapter-object.md))

    -   返回的值**MmGetMdlVirtualAddress**如果这是首次调用**MapTransfer**为当前的 IRP

        否则，该驱动程序将提供的已更新*CurrentVa*值，指示要执行的下一步物理到逻辑映射。 (如何计算的已更新*CurrentVa*稍后在本部分中介绍。)

    -   指向一个变量 (*长度*)，指示此传输的字节数

        如果驱动程序已足够映射寄存器传输单个 DMA 操作中的所有请求的数据并对其 DMA 操作，没有特定于设备的约束*长度*可以设置的值为**长度**中的驱动程序的 I/O 堆栈 IRP 的位置。 最多可以输入的长度 （字节） (页面\_大小\* *NumberOfMapRegisters*返回**IoGetDmaAdapter**)。 否则，该驱动程序必须拆分请求中所述[拆分传输请求](splitting-dma-transfer-requests.md)，并且必须更新的值*长度*在后续调用**MapTransfer**的当前 IRP。

    -   一个布尔值 (*WriteToDevice*)，指示在传输操作 （为 true，则将数据从内存转移到设备） 的方向

4.  *AdapterControl*例程将设置为 DMA 操作设备。

5.  *AdapterControl*例程返回**DeallocateObjectKeepRegisters**。

如果该驱动程序必须调用**MapTransfer**不止一次，以满足当前的 IRP，它会提供相同的适配器对象指针*Mdl*指针*MapRegisterBase*处理，和传输中的每个调用方向**MapTransfer**。 但是，必须提供该驱动程序更新*CurrentVa*并*长度*到其第二个和后续调用中的值**MapTransfer**。 使用以下公式来计算这些值：

-   *CurrentVa* = *CurrentVa* + (*长度*在前面的调用中请求**MapTransfer**)

-   *长度*= 最小值 (剩余**长度**要传输 (页\_大小\* *NumberOfMapRegisters*返回**IoGetDmaAdapter**))

每个驱动程序应保持其 DMA 传输有关的上下文信息取决于其特定设备的需求。 典型的上下文可能包括 MDL 中当前的虚拟地址 (*CurrentVa*)，与传输和可能是指向当前 IRP 的剩余字节数为止，传输的字节数。

对于具有散播-聚集功能的设备驱动程序*长度*参数**MapTransfer**是一个输入和输出参数。 返回从**MapTransfer**，它表示系统已映射的数据的字节数。 返回值，即*长度*，与返回的逻辑地址组合，指示主机总线适配器可用于此 DMA 操作中传输此段的逻辑地址的范围。

**请注意**  由于*长度*会被覆盖**MapTransfer**，请按照本实现原则：永远不会传递一个指向**长度**中的驱动程序的 I/O 堆栈位置作为 IRP*长度*参数**MapTransfer**如果设备支持散播-聚集。

执行此操作无法销毁当前 IRP，使其无法确定驱动程序是否已转移所有请求的数据中的值。

 

在每个 DMA 操作结束时，该驱动程序必须调用[ **FlushAdapterBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff545917)用一个有效的适配器的对象指针和*MapRegisterBase*句柄，以确保所有已传输数据，并释放当前 DMA 操作的物理到逻辑映射。 如果该驱动程序必须设置其他 DMA 操作，以满足当前 IRP，它必须调用**FlushAdapterBuffers**每个传输操作完成后。

当已完成所有请求的传输或驱动程序必须为 IRP 返回了错误状态时，该驱动程序应调用[ **FreeMapRegisters** ](https://msdn.microsoft.com/library/windows/hardware/ff546513)其最后一次调用后立即**FlushAdapterBuffers**为了获得最佳吞吐量主机总线适配器。 对其调用中**FreeMapRegisters**，该驱动程序必须传递它前面的调用中传递的适配器对象指针**AllocateAdapterChannel**。

 

 




