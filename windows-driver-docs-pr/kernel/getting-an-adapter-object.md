---
title: 获取适配器对象
description: 获取适配器对象
ms.assetid: 2af4ac28-b3c0-4e46-afb1-9c6897c67f03
keywords:
- 适配器对象 WDK 内核，入门
- DEVICE_DESCRIPTION
- DMA_OPERATIONS
- DMA 传输 WDK 内核，适配器对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 519b184bf177a79ba04d9c6f0f1f8a200c94f176
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386032"
---
# <a name="getting-an-adapter-object"></a>获取适配器对象





在设备启动时调用的驱动程序，使用系统或总线 master DMA [ **IoGetDmaAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter)获得到的适配器对象的指针并确定每个映射寄存器可用的最大数目传输操作。 当驱动程序调用**IoGetDmaAdapter**，I/O 管理器中，依次调用 HAL，若要获取所需的特定于平台的信息。

驱动程序必须提供某些信息中的系统定义[**设备\_说明**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_description)中对其调用结构**IoGetDmaAdapter**。 驱动程序必须使用[ **RtlZeroMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlzeromemory)初始化**设备\_说明**用零之前在其中设置值的结构。

所需的数据包括有关功能的驱动程序的设备，例如设备是总线主控形状，如果它具有散播-聚集功能和多少个字节的数据一次可以传输设备的信息 (**MaximumLength**).

所需的设备说明数据还包括特定于平台的信息，如主总线设备驱动程序控制的总线的特定于平台和系统分配数。 驱动程序可以通过调用来获取此信息[ **IoGetDeviceProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)。

**设备\_说明**结构包含可能会为某些 DMA 的设备或驱动程序不相关的某些字段。 例如， **BusNumber** WDM 驱动程序中不使用字段。 每个驱动程序应提供值的相关结构成员和应设置为零的所有其他成员值。

从属设备的驱动程序不应将传递 **，则返回 TRUE**中**ScatterGather**字段，除非设备是否能够等待时请求必须分解囿系统 DMA 控制器为两个或多个 DMA 的操作。

**IoGetDmaAdapter**返回一个指针，这两个适配器对象和特定于平台的或特定于设备的值，该值指示多少映射到寄存器是适用于每个 DMA 传输操作的适配器对象。

返回的适配器对象包含可以访问的驱动程序的三个字段：

-   版本号 (**版本**)

-   大小 (**大小**)

-   指向[ **DMA\_OPERATIONS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_dma_operations)结构 (**DmaOperations**)

**DMA\_OPERATIONS**结构包含指向该驱动程序必须使用执行其设备上的 DMA 操作的函数的指针的表。 函数是这种数据结构; 中的指针只能通过访问驱动程序不能通过名称直接调用它们。 (请注意，这些例程替换**Hal * Xxx*** 支持在以前版本的 Windows NT 的例程。 若要确保旧驱动程序的兼容性，wdm.h 中和 Ntddk.h 标头文件提供宏，并已过时的名称，但新的驱动程序应始终调用通过数据结构的函数。）

从设备和平台而异的映射寄存器的数量。 通常情况下，HAL 分配数的映射寄存器根据以下条件：

-   如果可能，HAL 返回的值一个映射寄存器的数量超过所需传输**MaximumLength**字节，驱动程序的调用中指定**IoGetDmaAdapter**。

-   否则，HAL 返回是尽可能特定平台大为较小值。

换而言之，HAL 足够映射寄存器来最大化 DMA 吞吐量为其设备，通常会为每个驱动程序，但是 HAL 可在某些 Windows 平台上返回较小的值。 则驱动程序将获取的请求，映射寄存器的数量，因此驱动程序应始终检查返回的值不能保证。

DMA 的设备驱动程序必须为适配器对象指针提供存储和*NumberOfMapRegisters*返回的值**IoGetDmaAdapter**。 此指针是使用 DMA 的系统提供支持例程所需的参数。 因为其中许多支持例程必须在调用在 IRQL = 调度\_级别，必须驻留的驱动程序分配的存储。 大多数 DMA 驱动程序提供必要的存储中[设备扩展](device-extensions.md)。 但是，存储可以是在控制器扩展如果驱动程序也使用[控制器对象](using-controller-objects.md)或驱动程序分配的非分页缓冲池。 请参阅[分配系统空间内存](allocating-system-space-memory.md)并[管理硬件优先级](managing-hardware-priorities.md)有关详细信息。

DMA 的所有操作完成后，驱动程序，它将调用[ **PutDmaAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pput_dma_adapter)来释放该适配器对象。

以下各节 ([使用系统 DMA](using-system-dma.md)并[使用总线 Master DMA](using-bus-master-dma.md)) 描述的 DMA 的设备使用支持例程来满足传输请求的方式整体化驱动程序。 这些部分假定该驱动程序有以下：

-   一种标准[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)例程，而不是设置和管理内部队列的 Irp

-   若要拆分为其注册的映射数目不足的传输请求内部例程

-   任何特定于设备的 DMA 约束

换而言之，下列各节介绍驱动程序的 DMA 操作，可能的最简单方法，但单个驱动程序不一定使用同样的技术。 DMA 设备的任何驱动程序的驱动程序例程应拆分大型 DMA 传输请求依赖于驱动程序模型 (类/端口或整体)，该驱动程序和任何特定于设备的 DMA 约束上设备的功能，必须处理。

 

 




