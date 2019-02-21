---
title: 批筛选器
description: 批筛选器
ms.assetid: 9e364c8f-55c3-4ec9-a9ce-9ee0f6a0746b
keywords:
- 音频筛选器 WDK 音频，批
- 批筛选器 WDK 音频
- 筛选器 WDK 音频，批
- 批呈现筛选器 WDK 音频
- 批捕获筛选器 WDK 音频
- 呈现波形音频 WDK 音频
- 捕获波形音频 WDK 音频
- WaveRT WDK 音频筛选器
- WavePci WDK 音频筛选器
- WaveCyclic WDK 音频筛选器
- WaveRT、 筛选器
- WavePci、 筛选器
- 音频设备 WaveCyclic
- WaveCyclic、 筛选器
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6c32ab24051c34ffe8cf8f265baaabdc5fa44880
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544655"
---
# <a name="wave-filters"></a>批筛选器


## <span id="wave_filters"></span><span id="WAVE_FILTERS"></span>


批的筛选器表示呈现和/或捕获波形格式的数字音频数据的设备。 应用程序通常访问这些设备的功能，通过 DirectSound API 或通过 Microsoft Windows 多媒体 waveOut*Xxx*和 waveIn*Xxx*函数。 WDM 音频驱动程序可以支持的波形格式信息，请参阅[ **WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff538799)并[ **WAVEFORMATEXTENSIBLE**](https://msdn.microsoft.com/library/windows/hardware/ff538802)。

一个*批呈现*筛选器作为输入接收批数字音频流，并输出 （到扬声器或外部 mixer 一组） 模拟音频信号或数字音频流 （例如 S/PDIF 连接器）。

一个*批捕获*模拟音频信号 （从麦克风或输入插孔中） 或 （从 S/PDIF 连接器，例如） 数字流筛选器收到作为输入。 相同的筛选器输出包含数字音频数据的批流。

单个批筛选器可同时执行呈现和捕获。 这种类型的筛选器可能，例如，表示可以播放音频通过演讲者和录制音频的一组通过麦克风在同一时间的音频设备。 或者，批呈现和批捕获硬件可能表示为单独的批筛选器，如中所述[动态音频子设备](dynamic-audio-subdevices.md)。

音频适配器驱动程序通过硬件供应商实现适配器驱动程序，与系统实现的波形端口驱动程序的一部分将批微型端口驱动程序绑定，从而形成批筛选器。 微型端口驱动程序处理的批筛选器中，所有特定于硬件的操作和端口驱动程序管理的所有泛型的批筛选器函数。

PortCls 系统驱动程序 (Portcls.sys) 实现三个波形端口驱动程序：WaveRT、 WavePci 和 WaveCyclic。

三种类型的批筛选器操作，如下所示：

-   一个*WaveRT*筛选器为批的数据分配一个缓冲区，并使该缓冲区到用户模式下客户端直接访问。 缓冲区可以包含连续的或者非连续内存块的能力，具体取决于批设备的硬件功能。 客户端访问作为一个连续的虚拟内存块的缓冲区。 缓冲区是循环，这意味着，当 （适用于呈现） 的设备的读取或写入 （对于捕获） 指针达到缓冲区的末尾时，会自动换行围绕到缓冲区的开头。

-   一个*WavePci*筛选器直接访问客户端的缓冲区。 尽管客户端访问作为单个的连续未分配的虚拟内存块的缓冲区，WavePci 筛选器必须访问作为一系列可能非连续内存块的缓冲区。 块包含呈现或捕获流的后续部分会在设备上排队等候。 当设备的读取或写入指针达到一个块的末尾时，它将移到队列中的下一块的开头。

-   一个*WaveCyclic*筛选器分配一个缓冲区，包含单个的连续未分配为其输出 （对于呈现） 或 （对于捕获） 输入的缓冲区的内存块。 此缓冲区是循环的。 由于缓冲区不是直接访问的客户端，该驱动程序必须将驱动程序的循环缓冲区和客户端的用户模式缓冲区之间的数据复制。

WaveRT 孰优孰 WavePci 和 WaveCyclic。 与早期版本的 Windows 使用了 WavePci 和 WaveCyclic。

WaveRT 筛选器可以表示系统总线，如 PCI 或 PCI Express 驻留的音频设备。 通过 WaveCyclic WaveRT 筛选器或 WavePci 筛选器的主要优点是 WaveRT 筛选器允许用户模式下客户端直接与音频硬件的音频数据交换。 与此相反，WaveCyclic 和 WavePci 筛选器这两个需要定期软件干预驱动程序，这会增加音频流的延迟。 此外，音频设备使用或不分散/聚拢 DMA 功能可以表示为 WaveRT 筛选器。 有关详细信息，请参阅[波形端口驱动程序进行实时流式处理音频](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/WaveRTport.doc)白皮书。


### <a name="span-idwavertfilterspanspan-idwavertfilterspanwavert-filters"></a><span id="wavert_filter"></span><span id="WAVERT_FILTER"></span>WaveRT 筛选器

WaveRT 筛选器作为端口/微型端口驱动程序对实现。 在 Windows Vista 及更高版本，WaveRT 筛选器工厂，如下所示创建 WaveRT 筛选器：

-   它实例化 WaveRT 微型端口驱动程序对象。

-   它通过调用实例化 WaveRT 端口驱动程序对象[ **PcNewPort** ](https://msdn.microsoft.com/library/windows/hardware/ff537715)使用的 GUID 值**CLSID\_PortWaveRT**。

-   它将调用端口驱动程序[ **IPort::Init** ](https://msdn.microsoft.com/library/windows/hardware/ff536943)方法绑定到端口驱动程序的微型端口驱动程序。

中的代码示例[子创建](subdevice-creation.md)说明了此过程。 通过与其他通信的端口和微型端口驱动程序及其[IPortWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536920)并[IMiniportWaveRT](https://msdn.microsoft.com/library/windows/hardware/ff536737)接口。

有关详细信息，请参阅[波形端口驱动程序进行实时流式处理音频](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/WaveRTport.doc)白皮书。

### <a name="span-idinformationforpreviousversionsofwindowsspanspan-idinformationforpreviousversionsofwindowsspanspan-idinformationforpreviousversionsofwindowsspaninformation-for-previous-versions-of-windows"></a><span id="Information_for_previous_versions_of_Windows"></span><span id="information_for_previous_versions_of_windows"></span><span id="INFORMATION_FOR_PREVIOUS_VERSIONS_OF_WINDOWS"></span>对于早期版本的 Windows 的信息

**对于早期版本的 Windows WaveCyclic 信息**

WaveCyclic 筛选器可以表示连接到系统总线，例如 ISA、 PCI、 PCI Express，或 PCMCIA 音频设备。 名称"WavePci"可以看出，WavePci 筛选器通常表示连接到 PCI 总线的设备，尽管从原理上讲，WavePci 设备可能会改为连接到 ISA 总线，例如。 与不同的是受 WaveCyclic 的简单设备，支持的 WavePci 设备必须具有散播-聚集 DMA 功能。 驻留在 PCI 总线上，但缺少散播-聚集的音频设备为 WaveCyclic 筛选器，但不能作为 WavePci 筛选器，可以表示 DMA。

**对于早期版本的 Windows WavePci 信息**

WavePci 设备能够执行散播-聚集 DMA 传输到或从缓冲区，也可位于任意内存地址和的开头和结尾任意字节对齐。 与此相反，WaveCyclic 设备 DMA 硬件要求仅能够将数据移到或从设备的微型端口驱动程序分配一个缓冲区。 WaveCyclic 微型端口驱动程序可以随意分配一个循环缓冲区，满足其 DMA 通道的功能有限。 例如，典型的 WaveCyclic 设备 DMA 通道可能需要满足以下限制的缓冲区：

-   在某些区域中的物理地址空间位于缓冲区。

-   缓冲区是在物理和虚拟地址空间中连续的。

-   缓冲区开始和结束甚至四个或 8 字节边界上。

由于这种简单性，但是，WaveCyclic 设备必须依赖于数据的软件复制到或从循环缓冲区，而 WavePci 设备依赖于的 DMA 硬件散播-聚集功能，若要避免此类复制。 这就是 Irp 波形音频数据交付到呈现设备或检索数据，从捕获设备附带数据缓冲区和每个这些缓冲区包含音频流的一部分被呈现或捕获。 WavePci 设备是能够通过其散播-聚集 DMA 引擎直接访问这些缓冲区而 WaveCyclic 设备需要从 IRP，数据将复制到其循环缓冲区，反之亦然。

### <a name="span-idwavepcifilterspanspan-idwavepcifilterspanwavepci-filters"></a><span id="wavepci_filter"></span><span id="WAVEPCI_FILTER"></span>WavePci 筛选器

**注意：对于早期版本的 Windows WavePci 信息**

作为端口/微型端口驱动程序对实现 WavePci 筛选器。 WavePci 筛选器工厂创建 WavePci 筛选器，如下所示：

-   它实例化 WavePci 微型端口驱动程序对象。

-   它通过调用实例化 WavePci 端口驱动程序对象[ **PcNewPort** ](https://msdn.microsoft.com/library/windows/hardware/ff537715)使用的 GUID 值**CLSID\_PortWavePci**。

-   它将调用端口驱动程序[ **IPort::Init** ](https://msdn.microsoft.com/library/windows/hardware/ff536943)方法绑定到端口驱动程序的微型端口驱动程序。

中的代码示例[子创建](subdevice-creation.md)说明了此过程。 通过与其他通信的端口和微型端口驱动程序及其[IPortWavePci](https://msdn.microsoft.com/library/windows/hardware/ff536905)并[IMiniportWavePci](https://msdn.microsoft.com/library/windows/hardware/ff536724)接口。

有关详细信息，请参阅[WavePci 设备的实现问题](implementation-issues-for-wavepci-devices.md)。

### <a name="span-idwavecyclicfilterspanspan-idwavecyclicfilterspanwavecyclic-filters"></a><span id="wavecyclic_filter"></span><span id="WAVECYCLIC_FILTER"></span>WaveCyclic 筛选器

**注意：对于早期版本的 Windows WaveCyclic 信息**

作为端口/微型端口驱动程序对实现 WaveCyclic 筛选器。 WaveCyclic 筛选器工厂创建 WaveCyclic 筛选器，如下所示：

-   它实例化 WaveCyclic 微型端口驱动程序对象。

-   它通过调用实例化 WaveCyclic 端口驱动程序对象[ **PcNewPort** ](https://msdn.microsoft.com/library/windows/hardware/ff537715)使用的 GUID 值**CLSID\_PortWaveCyclic**。

-   它将调用端口驱动程序[ **IPort::Init** ](https://msdn.microsoft.com/library/windows/hardware/ff536943)方法绑定到端口驱动程序的微型端口驱动程序。

中的代码示例[子创建](subdevice-creation.md)说明了此过程。 通过与其他通信的端口和微型端口驱动程序及其[IPortWaveCyclic](https://msdn.microsoft.com/library/windows/hardware/ff536899)并[IMiniportWaveCyclic](https://msdn.microsoft.com/library/windows/hardware/ff536714)接口。

WaveCyclic 筛选器的循环缓冲区始终包含虚拟内存的连续块。 端口驱动程序的实现[ **IDmaChannel::AllocateBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff536553)方法始终分配物理和虚拟内存地址空间中是连续的缓冲区。 如果前面曾经提到，WaveCyclic 设备的 DMA 引擎实施缓冲区内存的其他约束，微型端口驱动程序可以自由地实现其自己的缓冲区分配方法，以满足这些约束。

要求提供较大的缓冲区 （例如，八个物理上连续内存页） 的 WaveCyclic 微型端口驱动程序应准备好结清对较小的缓冲区大小，如果操作系统拒绝原始请求。 音频设备可能偶尔会卸载并重新加载来重新平衡系统资源 (请参阅[停止设备来重新平衡资源](https://msdn.microsoft.com/library/windows/hardware/ff563877))。

调用具有内置的总线主控 DMA 硬件的 WaveCyclic 设备*主设备*。 或者，可以是 WaveCyclic 设备*从属设备*没有内置的 DMA 硬件功能。 从属设备必须依赖于系统的 DMA 控制器来执行它要求任何数据传输。 有关主和从属设备的详细信息，请参阅[IDmaChannel](https://msdn.microsoft.com/library/windows/hardware/ff536547)并[IDmaChannelSlave](https://msdn.microsoft.com/library/windows/hardware/ff536548)。

微型端口驱动程序可以实现其自己的 DMA 通道对象而不是使用创建的其中一个端口驱动程序的默认 DMA 通道对象 WaveCyclic 的新建*Xxx*DmaChannel 方法：

[**IPortWaveCyclic::NewMasterDmaChannel**](https://msdn.microsoft.com/library/windows/hardware/ff536900)

[**IPortWaveCyclic::NewSlaveDmaChannel**](https://msdn.microsoft.com/library/windows/hardware/ff536902)

适配器驱动程序的自定义[IDmaChannel](https://msdn.microsoft.com/library/windows/hardware/ff536547)实现可以执行自定义处理数据以满足特殊硬件约束。 例如，Windows 多媒体函数使用波形格式中的 16 位样本都始终有符号值，但可能会呈现音频硬件设计以改为使用无符号的 16 位值。 在这种情况下，该驱动程序的自定义[ **IDmaChannel::CopyTo** ](https://msdn.microsoft.com/library/windows/hardware/ff536558)方法可以编写将签名的源值转换为硬件要求的无符号的目标值。 尽管此方法也可用于解决硬件设计缺陷，但它可以也会产生软件开销显著的成本。

有关实现其自己的 DMA 通道对象的驱动程序的示例，请参阅 WDK 中的 Sb16 示例音频适配器。 如果重写常量\_DMA\_通道被定义为**TRUE**，在源代码中的条件编译语句启用的一种专有实现[IDmaChannel](https://msdn.microsoft.com/library/windows/hardware/ff536547)对象，该驱动程序使用来取代默认 IDmaChannel 对象从 IPortWaveCyclic::New*Xxx*DmaChannel 调用。

 

 




