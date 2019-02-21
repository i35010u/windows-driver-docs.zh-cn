---
title: DMA 通道对象
description: DMA 通道对象
ms.assetid: 2064bbdf-62b7-454f-8764-b2aa21636c02
keywords:
- 帮助程序对象 WDK 音频，DMA 通道对象
- DMA 通道对象 WDK 音频
- 主设备 WDK 音频
- 从属设备 WDK 音频
- IDmaChannel 接口
- 通道对象 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2dcafb093a09c729eaec0850d4dd1f74d1c5b46d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541775"
---
# <a name="dma-channel-objects"></a>DMA 通道对象


## <span id="dma_channel_objects"></span><span id="DMA_CHANNEL_OBJECTS"></span>


PortCls 系统驱动程序实现[IDmaChannel](https://msdn.microsoft.com/library/windows/hardware/ff536547)并[IDmaChannelSlave](https://msdn.microsoft.com/library/windows/hardware/ff536548)为了方便 WaveCyclic 和 WavePci 微型端口驱动程序的接口。 **IDmaChannel**表示 DMA 通道以及其关联的 DMA 缓冲区和缓冲区使用情况参数。 此外，WaveCyclic 微型端口驱动程序使用**IDmaChannelSlave**管理从属设备 DMA 通道。 **IDmaChannelSlave**继承自**IDmaChannel**。 有关控制 DMA 操作的信息，请参阅[适配器对象和 DMA](https://msdn.microsoft.com/library/windows/hardware/ff540519)。

**IDmaChannel**对象将封装以下：

-   主数据库或从属设备 DMA 通道

-   与通道相关联的数据缓冲区

-   描述通道的使用方式的信息

端口和微型端口驱动程序使用 DMA 通道对象进行通信就 DMA 通道使用情况的信息。 通常情况下，微型端口驱动程序分配一组 DMA 通道在初始化期间或在流的创建过程。 新流期间，微型端口驱动程序指示端口驱动程序将为流使用哪些 DMA 通道对象。

DMA 通道对象可以创建主数据库或从属的设备：

-   从属设备没有内置的 DMA 硬件功能，并且必须依赖于系统的 DMA 控制器来执行设备要求任何数据传输。

-   主设备使用其自己总线主控 DMA 硬件系统总线上执行数据传输。

有关使用从属的 DMA 通道对象 WaveCyclic 设备的一个示例，请参阅 Sb16 示例音频驱动程序中 Microsoft Windows Driver Kit (WDK)。 主 DMA 通道对象是略高于 backboard 共享 DMA 通道之间的端口和微型端口驱动程序有关的信息。 有关主和从属设备的详细信息，请参阅[适配器对象简介](https://msdn.microsoft.com/library/windows/hardware/ff547986)。

主数据库或从属的设备的 DMA 通道对象公开了以下：

-   适配器对象

-   驱动程序和 DMA 硬件可以共享单个常见缓冲区

-   一个缓冲区大小值，可以查询和更改

*适配器对象*是一个用于 DMA 适配器结构*物理设备对象 (PDO)*。 微型端口驱动程序通过调用以下方法之一创建 DMA 通道对象时，自动创建的适配器对象：

[**IPortWavePci::NewMasterDmaChannel**](https://msdn.microsoft.com/library/windows/hardware/ff536916)

[**IPortWaveCyclic::NewMasterDmaChannel**](https://msdn.microsoft.com/library/windows/hardware/ff536900)

[**IPortWaveCyclic::NewSlaveDmaChannel**](https://msdn.microsoft.com/library/windows/hardware/ff536902)

该方法[ **IDmaChannel::GetAdapterObject** ](https://msdn.microsoft.com/library/windows/hardware/ff536560)可用于获取该适配器对象的指针。

适配器驱动程序还可以调用[ **PcNewDmaChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff537712)函数来创建 DMA 通道对象，但此函数是更难使用比**IPortWave*Xxx*:: 新建*Xxx*DmaChannel**调用，因为调用方必须显式指定一个设备对象和其他上下文信息。

对于从属的设备，DMA 通道[ **IDmaChannel::TransferCount** ](https://msdn.microsoft.com/library/windows/hardware/ff536565)方法返回的最大传输大小 ( *MapSize*参数) 这是对调用中指定[ **IDmaChannelSlave::Start**](https://msdn.microsoft.com/library/windows/hardware/ff536550)。 此外，该适配器对象提供了用于操作和查询 DMA 设备的一些方法。 这些方法均不是对主 DMA 通道有意义。

[**IDmaChannel::AllocateBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff536553)并[ **IDmaChannel::FreeBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff536559)用于管理与 DMA 通道对象相关联的单个常见缓冲区。 分配给对象缓冲区被保证为可访问驱动程序 （使用内核虚拟内存地址） 和 DMA 设备 （与物理内存地址）。 此外，则缓冲区将以物理上连续。 通常情况下，最佳策略是微型端口驱动程序初始化期间分配 DMA 缓冲区，当物理上连续内存最大量。 [**IDmaChannel::AllocatedBufferSize** ](https://msdn.microsoft.com/library/windows/hardware/ff536554)调用中指定了返回的缓冲区的大小**IDmaChannel::AllocateBuffer**。

[**IDmaChannel::MaximumBufferSize** ](https://msdn.microsoft.com/library/windows/hardware/ff536561)指示可以使用的实际最大缓冲区大小。 如果已分配的大小不是页面大小的偶数倍，这可能会超过分配的大小。 可能会分配的大小小于如果 DMA 设备不能支持传输的已分配的大小。 [**IDmaChannel::BufferSize** ](https://msdn.microsoft.com/library/windows/hardware/ff536556)并[ **IDmaChannel::SetBufferSize** ](https://msdn.microsoft.com/library/windows/hardware/ff536563)用于查询和设置要用于 DMA 传输的缓冲区的大小。 当分配缓冲区时，缓冲区大小设置为最大缓冲区大小。 初始化后，端口驱动程序和微型端口驱动程序有机会更改的缓冲区大小或发现其当前值。 微型端口驱动程序使用的结果**IDmaChannel::BufferSize** DMA 通道启动时确定 DMA 操作的传输大小。 [**IDmaChannel::SystemAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff536564)并[ **IDmaChannel::PhysicalAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff536562)用于分别获取缓冲区中的虚拟和物理地址。

[**IDmaChannel::CopyTo** ](https://msdn.microsoft.com/library/windows/hardware/ff536558)并[ **IDmaChannel::CopyFrom** ](https://msdn.microsoft.com/library/windows/hardware/ff536557)向 / 从 DMA 缓冲区复制示例数据。 WaveCyclic 端口驱动程序调用这些方法来将音频数据的应用程序缓冲区和微型端口驱动程序的循环缓冲区之间复制。

DMA 缓冲区一定不用于传输流的数据。 对于 WavePci 端口驱动程序，流的数据传送到 （或从检索） 微型端口驱动程序，因为散播-聚集映射的列表。 但是，微型端口驱动程序可能仍利用 DMA 缓冲区作为适配器驱动程序进行通信的共享的内存空间。

端口驱动程序提供函数，它们可用于创建 DMA 通道的微型端口驱动的程序。 除非端口驱动程序的说明中另有说明，否则它不是绝对必要，若要使用 DMA 端口驱动程序从分配的对象。 端口驱动程序只需要一个指向**IDmaChannel**接口，它支持其所需的方法。 检查端口驱动程序需要的 DMA 通道方法列表每个端口驱动程序的文档。

通常情况下，最简单的方法是使用端口驱动程序实现的 DMA 通道分配函数。 在极少数情况下，微型端口驱动程序开发人员可能需要实施自己的 DMA 通道对象以满足其特定的适配器的特殊要求。 这有时需要一个新的对象的实现。 在其他情况下，它就足以具有微型端口驱动程序的流对象公开**IDmaChannel**接口并实现 DMA 通道方法本身。

**IDmaChannel**接口支持以下方法：

[**IDmaChannel::AllocateBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536553)

[**IDmaChannel::AllocatedBufferSize**](https://msdn.microsoft.com/library/windows/hardware/ff536554)

[**IDmaChannel::BufferSize**](https://msdn.microsoft.com/library/windows/hardware/ff536556)

[**IDmaChannel::CopyFrom**](https://msdn.microsoft.com/library/windows/hardware/ff536557)

[**IDmaChannel::CopyTo**](https://msdn.microsoft.com/library/windows/hardware/ff536558)

[**IDmaChannel::FreeBuffer**](https://msdn.microsoft.com/library/windows/hardware/ff536559)

[**IDmaChannel::GetAdapterObject**](https://msdn.microsoft.com/library/windows/hardware/ff536560)

[**IDmaChannel::MaximumBufferSize**](https://msdn.microsoft.com/library/windows/hardware/ff536561)

[**IDmaChannel::PhysicalAddress**](https://msdn.microsoft.com/library/windows/hardware/ff536562)

[**IDmaChannel::SetBufferSize**](https://msdn.microsoft.com/library/windows/hardware/ff536563)

[**IDmaChannel::SystemAddress**](https://msdn.microsoft.com/library/windows/hardware/ff536564)

[**IDmaChannel::TransferCount**](https://msdn.microsoft.com/library/windows/hardware/ff536565)

**IDmaChannelSlave**接口扩展**IDmaChannel**通过添加以下方法：

[**IDmaChannelSlave::ReadCounter**](https://msdn.microsoft.com/library/windows/hardware/ff536549)

[**IDmaChannelSlave::Start**](https://msdn.microsoft.com/library/windows/hardware/ff536550)

[**IDmaChannelSlave::Stop**](https://msdn.microsoft.com/library/windows/hardware/ff536551)

[**IDmaChannelSlave::WaitForTC**](https://msdn.microsoft.com/library/windows/hardware/ff536552)

 

 




