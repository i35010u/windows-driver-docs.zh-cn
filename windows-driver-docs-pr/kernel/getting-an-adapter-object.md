---
title: 获取适配器对象
description: 获取适配器对象
ms.assetid: 2af4ac28-b3c0-4e46-afb1-9c6897c67f03
keywords:
- 适配器对象 WDK 内核，获取
- DEVICE_DESCRIPTION
- DMA_OPERATIONS
- DMA 传输 WDK 内核，适配器对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a11da255ede82f86a705dd1673e9b428313270e
ms.sourcegitcommit: 057b72e8a44ba8f4282e072edc7be0b7e9341d2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89412440"
---
# <a name="getting-an-adapter-object"></a>获取适配器对象





设备启动时，使用系统或总线主控 DMA 的驱动程序会调用 [**IoGetDmaAdapter**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdmaadapter) 来获取指向适配器对象的指针，并确定每个传输操作可用的最大映射寄存器数。 当驱动程序调用 **IoGetDmaAdapter**时，i/o 管理器反过来会调用 HAL 以获取所需的特定于平台的信息。

在对**IoGetDmaAdapter**的调用中，驱动程序必须在系统定义的[**设备 \_ 说明**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_description)结构中提供某些信息。 在设置中的值之前，驱动程序必须使用 [**RtlZeroMemory**](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlzeromemory) 来初始化 **设备 \_ 说明** 结构。

所需的数据包括有关驱动程序的设备功能的信息，例如，设备是否为总线主机（如果该设备具有散点/收集功能）以及设备可以一次传输的数据量 (**MaximumLength**) 。

所需的设备描述数据还包括特定于平台的信息，如总线-主设备的驱动程序的特定于平台和系统分配的总线数。 驱动程序可以通过调用 [**IoGetDeviceProperty**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)来获取此信息。

**设备 \_ 说明**结构包括一些可能与某些 DMA 设备或驱动程序不相关的字段。 例如，WDM 驱动程序中不使用 **BusNumber** 字段。 每个驱动程序都应为相关结构成员提供值，并应将所有其他成员的值设置为零。

在**ScatterGather**字段中，从属设备的驱动程序不应传递**TRUE** ，除非该设备在必须将请求分为两个或更多 DMA 操作时等待系统 DMA 控制器 reprogrammed。

**IoGetDmaAdapter** 返回指向适配器对象的指针和特定于平台的或特定于设备的值，指示每个 DMA 传输操作的适配器对象有多少个映射寄存器。

返回的适配器对象包含三个可供驱动程序访问的字段：

-   版本编号 (**版本**) 

-   大小 (**大小**) 

-   指向 [**DMA \_ 操作**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_operations) 结构 (**DmaOperations** 的指针) 

**DMA \_ 操作**结构包含一个指针表，这些指针指向驱动程序必须用于在其设备上执行 DMA 操作的函数。 仅可通过此数据结构中的指针访问函数;驱动程序无法按名称直接调用它们。  (请注意，这些例程将替换以前版本的 Windows NT 中支持的 **Hal * Xxx*** 例程。 为了确保旧驱动程序的兼容性，Wdm 和 Ntddk 头文件提供了具有过时名称的宏，但新的驱动程序应始终通过数据结构调用函数。 ) 

映射寄存器的数量可能会因设备而异，也不同于平台。 通常，HAL 根据以下条件分配若干映射寄存器：

-   如果可能，HAL 将返回一个值，该值比传输 **MaximumLength** 字节所需的映射寄存器数多一，如驱动程序对 **IoGetDmaAdapter**的调用中所指定的那样。

-   否则，HAL 返回的值越小，就越适合特定平台。

换句话说，HAL 通常为每个驱动程序提供足够多的映射寄存器，以最大程度地提高其设备的 DMA 吞吐量，但 HAL 可以在某些 Windows 平台上返回较小的值。 不保证驱动程序将获得它所请求的映射寄存器的数目，因此，驱动程序应始终检查返回值。

任何 DMA 设备驱动程序必须为适配器对象指针和**IoGetDmaAdapter**返回的*NumberOfMapRegisters*值提供存储。 此指针是系统提供的用于 DMA 的支持例程的必需参数。 由于其中的许多支持例程必须以 IRQL = 调度级别调用 \_ ，所以，驱动程序分配的存储必须为驻留。 大多数 DMA 驱动程序在 [设备扩展](device-extensions.md)中提供必要的存储。 但是，如果驱动程序还使用 [控制器对象](./introduction-to-controller-objects.md) 或由驱动程序分配的非分页池，则存储可以位于控制器扩展中。 有关详细信息，请参阅 [分配系统空间内存](allocating-system-space-memory.md) 和 [管理硬件优先级](managing-hardware-priorities.md) 。

当驱动程序完成所有 DMA 操作时，它会调用 [**PutDmaAdapter**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pput_dma_adapter) 来释放适配器对象。

以下部分 [使用系统 dma](introduction-to-adapter-objects.md) 和 [使用总线主控 DMA](using-bus-master-dma.md)) 说明 DMA 设备的单一驱动程序如何使用支持例程来满足传输请求。 这些部分假定驱动程序具有以下各项：

-   标准 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程，而不是设置和管理 irp 的内部队列

-   拆分传输请求的内部例程，这些请求的映射寄存器数量不足

-   没有特定于设备的 DMA 约束

换句话说，这些部分描述了驱动程序 DMA 操作的最简单方法，但单个驱动程序并不一定要使用完全相同的技术。 对于 DMA 设备的任何驱动程序，哪些驱动程序例程应分割大型 DMA 传输请求取决于驱动程序模型 (类/端口或单一) 、设备的功能以及驱动程序必须处理的任何特定于设备的 DMA 约束。

 

