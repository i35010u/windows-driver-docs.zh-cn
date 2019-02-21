---
title: 为基于数据包的 DMA 设置系统 DMA 控制器
description: 为基于数据包的 DMA 设置系统 DMA 控制器
ms.assetid: 3a646169-1ea3-4844-b771-d08f4ddec460
keywords:
- DMA WDK 内核，基于数据包的系统
- 基于数据包的 DMA WDK 内核
- DMA 传输 WDK 内核，基于数据包的
- AllocateAdapterChannel
- MapTransfer
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f713a72bda7b8fa3be399233e14f6de9bed80b61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521014"
---
# <a name="setting-up-the-system-dma-controller-for-packet-based-dma"></a>为基于数据包的 DMA 设置系统 DMA 控制器





当[ **AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)将控制转移到的驱动程序[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)例程，该驱动程序"拥有"系统 DMA控制器和一组映射寄存器。 然后，该驱动程序必须设置传输操作中，DMA 控制器，如下图中所示。

![说明编程系统 dma 控制器的关系图](images/3dmaptsf.png)

如果该驱动程序有[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)例程， [ **AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)将传递一个指向**DeviceObject&gt;CurrentIrp**中*PIrp*参数*AdapterControl*例程。 如果，但是，该驱动程序管理其自身的 Irp 的队列，该驱动程序应作为上下文的一部分传递到包含指向当前 IRP *AdapterControl*。

上一图所示，该驱动程序的*AdapterControl*例程将 DMA 传输设置，如下所示：

1.  *AdapterControl*例程获取开始传输地址。 将满足 IRP，所需的初始传输*AdapterControl*例程调用[ **MmGetMdlVirtualAddress**](https://msdn.microsoft.com/library/windows/hardware/ff554539)，将指针传递到在 MDL **Irp-&gt;MdlAddress**，这对于此 DMA 传输描述缓冲区。

    **MmGetMdlVirtualAddress**返回驱动程序可用作索引的系统的物理地址传输应开始的位置的虚拟地址。

    如果 IRP 需要多个传输操作，该驱动程序将计算的已更新的起始地址，如在本部分后面所述。

2.  *AdapterControl*例程将返回的地址保存**MmGetMdlVirtualAddress**或在步骤 1 中计算。 此地址是必需的参数 (*CurrentVa*) 到[ **MapTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff554402)。

3.  *AdapterControl*例程调用**MapTransfer**若要设置系统 DMA 控制器，提供以下参数：

    -   所返回的适配器对象指针[ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)

    -   一个指针 (*Mdl*) 到在 MDL **Irp-&gt;MdlAddress**为当前的 IRP

    -   *MapRegisterBase*句柄传递给驱动程序的*AdapterControl*例程通过**AllocateAdapterChannel**

    -   值 (*CurrentVa*) 返回由**MmGetMdlVirtualAddress**如果这是首次调用**MapTransfer**的 IRP

        否则，该驱动程序将提供的已更新*CurrentVa*值，指示缓冲区下一个传输中操作应开始的位置。

    -   指向一个变量 (*长度*)，说明此传输的字节数

        如果驱动程序可以所有请求使用传输数据调用一次**MapTransfer**和其 DMA 操作，没有特定于设备的约束*长度*可以设置的值为**长度**在驱动程序的 I/O 堆栈 IRP 的位置。 以字节为单位的长度最多可以是 (页\_大小\* *NumberOfMapRegisters*返回[ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220))。 否则，该驱动程序必须拆分请求中所述[拆分传输请求](splitting-dma-transfer-requests.md)，并且必须更新的值*长度*在后续调用**MapTransfer**的当前 IRP。

    -   一个布尔值 (*WriteToDevice*)，指示在传输操作 （为 true，则传输系统内存中的数据复制到设备） 的方向

    **MapTransfer**返回逻辑地址。 使用系统 DMA 的驱动程序必须忽略此值。

4.  *AdapterControl*例程将设置为 DMA 操作设备。

5.  *AdapterControl*例程返回**KeepObject**。

该驱动程序时设备将指示其当前的 DMA 操作已完成，应调用[ **FlushAdapterBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff545917)，通常来自驱动程序的[ *DpcForIsr*](https://msdn.microsoft.com/library/windows/hardware/ff544079)例程。

*DpcForIsr*例程或完成 DMA 操作的另一个驱动程序例程调用**FlushAdapterBuffers**要确保任何数据缓存在系统 DMA 控制器不读取到系统内存或写出到设备。 此外必须调用的相同例程**MapTransfer**再次如有必要对系统的 DMA 控制器当前 IRP 的传输更多的数据。 同样，它必须调用**FlushAdapterBuffers**再次按照每个传输操作。

如果驱动程序必须调用**MapTransfer**不止一次为当前的 IRP，它提供了相同的适配器对象指针*Mdl*指针*MapRegisterBase*处理，并传输中的每个调用的方向。 但是，必须更新该驱动程序*CurrentVa*并*长度*之前第二个和任何后续调用的参数**MapTransfer**。 若要计算这些参数的每个更新的值，请使用以下公式：

-   *CurrentVa* = *CurrentVa* + (*长度*在前面的调用中请求**MapTransfer**)

-   *长度*= 最小值 (剩余**长度**要传输 (页\_大小\* *NumberOfMapRegisters*返回**IoGetDmaAdapter**))

每个驱动程序应保持其 DMA 传输有关的上下文信息取决于其特定设备的需求。 典型的上下文可能包括 MDL 中当前的虚拟地址 (*CurrentVa*)，传输到目前为止，要传输，可能是一个指向当前 IRP 和任何其他信息的剩余字节数的字节数。驱动程序编写者认为有用。

当请求的传输已完成，或如果该驱动程序必须为 IRP 返回的错误状态，该驱动程序应调用[ **FreeAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff546507)立即以发布适用于其他系统 DMA 控制器驱动程序和要使用此驱动程序。

 

 




