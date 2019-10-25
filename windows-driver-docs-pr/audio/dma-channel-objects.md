---
title: DMA 通道对象
description: DMA 通道对象
ms.assetid: 2064bbdf-62b7-454f-8764-b2aa21636c02
keywords:
- helper 对象 WDK 音频，DMA 通道对象
- DMA 通道对象 WDK 音频
- 主设备 WDK 音频
- 从属设备音响音频
- IDmaChannel 接口
- 通道对象 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b4b4ba0b9ce16ed8a9ebe5ee88926d37cfc1f08
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833470"
---
# <a name="dma-channel-objects"></a>DMA 通道对象


## <span id="dma_channel_objects"></span><span id="DMA_CHANNEL_OBJECTS"></span>


PortCls 系统驱动程序为 WaveCyclic 和 WavePci 微型端口驱动程序的优点实现了[IDmaChannel](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idmachannel)和[IDmaChannelSlave](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idmachannelslave)接口。 **IDmaChannel**表示 dma 通道及其关联的 dma 缓冲区和缓冲区用法参数。 此外，WaveCyclic 微型端口驱动程序使用**IDmaChannelSlave**管理从属设备的 DMA 通道。 **IDmaChannelSlave**继承自**IDmaChannel**。 有关控制 DMA 操作的详细信息，请参阅[适配器对象和 DMA](https://docs.microsoft.com/windows-hardware/drivers/kernel/adapter-objects-and-dma)。

**IDmaChannel**对象封装以下内容：

-   主设备或从属设备的 DMA 通道

-   与通道关联的数据缓冲区

-   描述如何使用通道的信息

端口和微型端口驱动程序使用 DMA 通道对象传达有关 DMA 通道使用情况的信息。 通常，微型端口驱动程序会在初始化期间或在创建流期间分配一组 DMA 通道。 在创建新流的过程中，微型端口驱动程序会告知端口驱动程序要将哪个 DMA 通道对象用于流。

可以为主设备或从属设备创建 DMA 通道对象：

-   从属设备没有内置 DMA 硬件功能，必须依赖系统 DMA 控制器执行设备所需的任何数据传输。

-   主设备使用自己的总线主控 DMA 硬件在系统总线上执行数据传输。

有关使用从属 DMA 通道对象的 WaveCyclic 设备的示例，请参阅 Microsoft Windows 驱动程序工具包（WDK）中的 Sb16 示例音频驱动程序。 主 DMA 通道对象只是一个 backboard，用于在端口和微型端口驱动程序之间共享 DMA 通道的相关信息。 有关主设备和从属设备的详细信息，请参阅[适配器对象简介](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-adapter-objects)。

主设备或从属设备的 DMA 通道对象公开以下内容：

-   适配器对象

-   驱动程序和 DMA 硬件可以共享的单个常见缓冲区

-   可以查询和更改的缓冲区大小值

*适配器对象*是*物理设备对象（PDO）* 的 DMA 适配器结构。 当微型端口驱动程序通过调用以下方法之一创建 DMA 通道对象时，将自动创建适配器对象：

[**IPortWavePci::NewMasterDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-newmasterdmachannel)

[**IPortWaveCyclic::NewMasterDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavecyclic-newmasterdmachannel)

[**IPortWaveCyclic::NewSlaveDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavecyclic-newslavedmachannel)

方法[**IDmaChannel：： GetAdapterObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-getadapterobject)可用于获取指向适配器对象的指针。

适配器驱动程序还可以调用[**PcNewDmaChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewdmachannel)函数来创建 DMA 通道对象，但此函数比**IPortWave*Xxx*：： New*Xxx*DmaChannel**调用更难使用，因为调用方必须显式指定设备对象和其他上下文信息。

对于从属设备的 DMA 通道， [**IDmaChannel：： TransferCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-transfercount)方法返回在调用[**IDmaChannelSlave：： Start**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannelslave-start)中指定的最大传输大小（ *MapSize*参数）。 此外，适配器对象还提供了一些操作和查询 DMA 设备的方法。 这些方法对于主 DMA 通道均无意义。

[**IDmaChannel：： AllocateBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-allocatebuffer)和[**IDmaChannel：： FreeBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-freebuffer)用于管理与 DMA 通道对象关联的单个公共缓冲区。 保证由对象分配的缓冲区可供驱动程序（包含内核虚拟内存地址）和 DMA 设备（包含物理内存地址）访问。 此外，缓冲区将是物理上连续的。 通常，最佳策略是在大量物理内存最大的情况下，在微型端口驱动程序初始化期间分配 DMA 缓冲区。 [**IDmaChannel：： AllocatedBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-allocatedbuffersize)返回在对**IDmaChannel：： AllocateBuffer**的调用中指定的缓冲区大小。

[**IDmaChannel：： MaximumBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-maximumbuffersize)指示可以使用的实际最大缓冲区大小。 如果分配的大小不是页面大小的偶数倍，则这可能会超出分配的大小。 如果 DMA 设备不支持传输分配的大小，则它可能小于分配的大小。 [**IDmaChannel：： BufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-buffersize)和[**IDmaChannel：： SetBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-setbuffersize)用于查询和设置要用于 DMA 传输的缓冲区大小。 分配缓冲区时，缓冲区大小设置为最大缓冲区大小。 初始化之后，端口驱动程序和微型端口驱动程序都有机会更改缓冲区大小或发现它的当前值。 小型端口驱动程序使用**IDmaChannel：： BufferSize**的结果来确定 dma 通道启动时 dma 操作的传输大小。 [**IDmaChannel：： SystemAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-systemaddress)和[**IDmaChannel：:P hysicaladdress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-physicaladdress)分别用于获取缓冲区的虚拟地址和物理地址。

[**IDmaChannel：： CopyTo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-copyto)和[**IDmaChannel：： CopyFrom**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-copyfrom)将示例数据复制到 DMA 缓冲区和从中复制。 WaveCyclic 端口驱动程序调用这些方法，以便在应用程序缓冲区和微型端口驱动程序的循环缓冲区之间复制音频数据。

DMA 缓冲区不一定用于传输流式处理数据。 对于 WavePci 端口驱动程序，流式处理数据将作为散点/集合映射的列表传送到（或从）微型端口驱动程序中检索。 但是，微型端口驱动程序仍可能将 DMA 缓冲区用作共享的内存空间，以便与适配器驱动程序通信。

端口驱动程序为微型端口驱动程序提供了可用于创建 DMA 通道的函数。 除非在端口驱动程序的说明中另有说明，否则不一定要使用从端口驱动程序分配的 DMA 对象。 端口驱动程序只需要一个指向**IDmaChannel**接口的指针，该接口支持其所需的方法。 请查看每个端口驱动程序的文档，以获取端口驱动程序所需的 DMA 通道方法的列表。

通常，最简单的方法是使用端口驱动程序实现的 DMA 通道分配函数。 在极少数情况下，微型端口驱动程序开发人员可能需要实现其自己的 DMA 通道对象，以满足特定适配器的特殊要求。 这有时需要实现新的对象。 在其他情况下，足以使微型端口驱动程序的流对象公开**IDmaChannel**接口并实现 DMA 通道方法本身。

**IDmaChannel**接口支持以下方法：

[**IDmaChannel::AllocateBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-allocatebuffer)

[**IDmaChannel::AllocatedBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-allocatedbuffersize)

[**IDmaChannel：： BufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-buffersize)

[**IDmaChannel：： CopyFrom**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-copyfrom)

[**IDmaChannel：： CopyTo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-copyto)

[**IDmaChannel::FreeBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-freebuffer)

[**IDmaChannel::GetAdapterObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-getadapterobject)

[**IDmaChannel::MaximumBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-maximumbuffersize)

[**IDmaChannel：:P hysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-physicaladdress)

[**IDmaChannel::SetBufferSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-setbuffersize)

[**IDmaChannel::SystemAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-systemaddress)

[**IDmaChannel::TransferCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-transfercount)

**IDmaChannelSlave**接口通过添加以下方法来扩展**IDmaChannel** ：

[**IDmaChannelSlave::ReadCounter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannelslave-readcounter)

[**IDmaChannelSlave：： Start**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannelslave-start)

[**IDmaChannelSlave：： Stop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannelslave-stop)

[**IDmaChannelSlave::WaitForTC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannelslave-waitfortc)

 

 




