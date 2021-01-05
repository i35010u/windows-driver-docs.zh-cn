---
title: 滤波器
description: 滤波器
keywords:
- 音频筛选器 WDK 音频，wave
- 波形筛选 WDK 音频
- 筛选 WDK 音频，wave
- 波形呈现筛选器 WDK 音频
- 波形捕获筛选 WDK 音频
- 渲染波形音频 WDK 音频
- 捕获波形音频 WDK 音频
- WaveRT 筛选 WDK 音频
- WavePci 筛选 WDK 音频
- WaveCyclic 筛选 WDK 音频
- WaveRT，筛选器
- WavePci，筛选器
- 音频设备，WaveCyclic
- WaveCyclic，筛选器
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: e25715f854b192a8b4dd04a9ca4d8d86ebd09e4a
ms.sourcegitcommit: 7bdf85c72841fbc2093c315f900c69d2eef6e3e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/23/2020
ms.locfileid: "97757890"
---
# <a name="wave-filters"></a>滤波器


## <span id="wave_filters"></span><span id="WAVE_FILTERS"></span>


波形筛选器代表呈现和/或捕获波格式数字音频数据的设备。 通常，应用程序可以通过 DirectSound API 或 Microsoft Windows 多媒体 waveOut *xxx* 和 waveIn *Xxx* 函数访问这些设备的功能。 有关 WDM 音频驱动程序可以支持的波形格式的信息，请参阅 [**WAVEFORMATEX**](/windows/win32/api/mmreg/ns-mmreg-waveformatex) 和 [**WAVEFORMATEXTENSIBLE**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)。

*波形渲染* 筛选器接收波形数字音频流作为输入，并将模拟音频信号 (输出到一组扬声器或外部混合器) 或 (到 S/PDIF 连接器的数字音频流（例如) ）。

*波形捕获* 筛选器以输入的形式接收从麦克风或输入插孔 (的模拟音频信号，或从 S/PDIF 连接器) 或数字流 (，例如) 。 同一筛选器输出包含数字音频数据的波形流。

单个波形筛选器可以同时执行呈现和捕获。 例如，这种类型的筛选器可能代表音频设备，可以通过一组扬声器播放音频，同时通过麦克风录制音频。 或者，波形渲染和波形捕获硬件可能会表示为不同的波滤波器，如 [动态音频 Subdevices](dynamic-audio-subdevices.md)中所述。

音频适配器驱动程序通过绑定波形微型端口驱动程序形成波形筛选器，该驱动程序将硬件供应商实现为适配器驱动程序的一部分，并使用系统实现的波形端口驱动程序。 微型端口驱动程序处理波形筛选器的所有特定于硬件的操作，端口驱动程序管理所有通用波形筛选器函数。

PortCls 系统驱动程序 ( # A0) 实现三个波形端口驱动程序： WaveRT、WavePci 和 WaveCyclic。

这三种类型的波形滤镜的操作如下所示：

-   *WaveRT* 筛选器为波数据分配一个缓冲区，并使该缓冲区可直接用于用户模式客户端。 根据波形设备的硬件功能，该缓冲区可包含连续或非连续的内存块。 客户端以连续的虚拟内存块的形式访问缓冲区。 缓冲区是循环的，这意味着当设备的读取 (呈现) 或写入 (以便捕获) 指针到达缓冲区的末尾时，它会自动环绕到缓冲区的开头。

-   *WavePci* 筛选器直接访问客户端的缓冲区。 尽管客户端以单个连续的虚拟内存块的形式访问缓冲区，但 WavePci 筛选器必须以一系列可能不连续的内存块的形式访问缓冲区。 包含呈现或捕获流的连续部分的块在设备上排队。 当设备的读取或写入指针到达一个块的末尾时，它将移到队列中下一个块的开头。

-   *WaveCyclic* 筛选器分配一个缓冲区，该缓冲区由单个连续的 (内存块组成，用于呈现) 或输入 (以便捕获) 缓冲区。 此缓冲区是循环的。 因为客户端不能直接访问该缓冲区，所以，驱动程序必须在驱动程序的循环缓冲区和客户端的用户模式缓冲区之间复制数据。

WaveRT 优先于 WavePci 和 WaveCyclic。 WavePci 和 WaveCyclic 用于 Windows 的早期版本。

WaveRT 筛选器可以代表位于系统总线上的音频设备，如 PCI 或 PCI Express。 通过 WaveCyclic 或 WavePci 筛选器的 WaveRT 筛选器的主要优点是 WaveRT 筛选器允许用户模式客户端直接与音频硬件交换音频数据。 相反，WaveCyclic 和 WavePci 筛选器都需要驱动程序定期进行软件干预，这会增加音频流的延迟时间。 此外，具有和不包含散播/聚集 DMA 功能的音频设备可表示为 WaveRT 筛选器。 有关详细信息，请参阅 [Real-Time 音频流式传输的 Wave 端口驱动程序](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/WaveRTport.doc) 白皮书。


### <a name="span-idwavert_filterspanspan-idwavert_filterspanwavert-filters"></a><span id="wavert_filter"></span><span id="WAVERT_FILTER"></span>WaveRT 筛选器

WaveRT 筛选器实现为端口/微型端口驱动程序对。 在 Windows Vista 和更高版本中，WaveRT 筛选器工厂创建 WaveRT 筛选器，如下所示：

-   它实例化 WaveRT 微型端口驱动程序对象。

-   它通过使用 GUID 值 **CLSID \_ PortWaveRT** 调用 [**PcNewPort**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)来实例化 WaveRT 端口驱动程序对象。

-   它调用端口驱动程序的 [**IPort：： Init**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init) 方法将微型端口驱动程序绑定到端口驱动程序。

[Subdevice 创建](subdevice-creation.md)中的代码示例演示了此过程。 端口和微型端口驱动程序通过其 [IPortWaveRT](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavert) 和 [IMiniportWaveRT](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavert) 接口相互通信。

有关详细信息，请参阅 [Real-Time 音频流式传输的 Wave 端口驱动程序](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/WaveRTport.doc) 白皮书。

### <a name="span-idinformation_for_previous_versions_of_windowsspanspan-idinformation_for_previous_versions_of_windowsspanspan-idinformation_for_previous_versions_of_windowsspaninformation-for-previous-versions-of-windows"></a><span id="Information_for_previous_versions_of_Windows"></span><span id="information_for_previous_versions_of_windows"></span><span id="INFORMATION_FOR_PREVIOUS_VERSIONS_OF_WINDOWS"></span>适用于以前版本的 Windows 的信息

**以前版本的 Windows 的 WaveCyclic 信息**

WaveCyclic 筛选器可以表示连接到系统总线的音频设备，如 ISA、PCI、PCI Express 或 PCMCIA。 如名称 "WavePci"，WavePci 筛选器通常表示连接到 PCI 总线的设备，但在原则上，WavePci 设备可能改为连接到 ISA 总线（例如）。 不同于 WaveCyclic 支持的更简单设备，WavePci 支持的设备必须具有散播/聚集 DMA 功能。 驻留在 PCI 总线上但缺少散播/聚集 DMA 的音频设备可表示为 WaveCyclic 筛选器，但不能表示为 WavePci 筛选器。

**以前版本的 Windows 的 WavePci 信息**

WavePci 设备能够执行与缓冲区的散播/聚集 DMA 传输，这些缓冲区可位于任意内存地址，并以任意字节对齐方式开始和结束。 与此相反，WaveCyclic 设备的 DMA 硬件只需能够将数据移入或移出设备的微型端口驱动程序分配的单个缓冲区。 WaveCyclic 微型端口驱动程序可自由分配一个可满足其 DMA 通道的有限功能的循环缓冲区。 例如，典型 WaveCyclic 设备的 DMA 通道可能需要满足以下限制的缓冲区：

-   缓冲区位于物理地址空间的某个区域。

-   缓冲区在物理和虚拟地址空间中是连续的。

-   缓冲区的开始和结束时间甚至是四个或八个字节的边界。

然而，为此简单起见，WaveCyclic 设备必须依赖于将数据复制到循环缓冲区或从循环缓冲区复制，而 WavePci 设备依赖于其 DMA 硬件的分散/收集功能来避免此类复制。 用于将波形音频数据传递到呈现设备或从捕获设备检索数据的 Irp 附带数据缓冲区，其中每个缓冲区都包含正在呈现或捕获的音频流的一部分。 WavePci 设备可以通过其散播/聚集 DMA 引擎直接访问这些缓冲区，而 WaveCyclic 设备要求将数据从 IRP 复制到其循环缓冲区，反之亦然。

### <a name="span-idwavepci_filterspanspan-idwavepci_filterspanwavepci-filters"></a><span id="wavepci_filter"></span><span id="WAVEPCI_FILTER"></span>WavePci 筛选器

**注意： Windows 以前版本的 WavePci 信息**

WavePci 筛选器实现为端口/微型端口驱动程序对。 WavePci 筛选器工厂创建 WavePci 筛选器，如下所示：

-   它实例化 WavePci 微型端口驱动程序对象。

-   它通过使用 GUID 值 **CLSID \_ PortWavePci** 调用 [**PcNewPort**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)来实例化 WavePci 端口驱动程序对象。

-   它调用端口驱动程序的 [**IPort：： Init**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init) 方法将微型端口驱动程序绑定到端口驱动程序。

[Subdevice 创建](subdevice-creation.md)中的代码示例演示了此过程。 端口和微型端口驱动程序通过其 [IPortWavePci](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavepci) 和 [IMiniportWavePci](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepci) 接口相互通信。

有关详细信息，请参阅 [WavePci 设备的实现问题](implementation-issues-for-wavepci-devices.md)。

### <a name="span-idwavecyclic_filterspanspan-idwavecyclic_filterspanwavecyclic-filters"></a><span id="wavecyclic_filter"></span><span id="WAVECYCLIC_FILTER"></span>WaveCyclic 筛选器

> [!NOTE]
> Microsoft 支持各种不同的环境。 本文介绍了 [Microsoft 风格的无偏差通信的 Microsoft 风格指南](/style-guide/bias-free-communication) 的术语参考。 本文中使用的词或短语的一致性是因为它当前出现在软件中。 当软件更新为删除语言时，本文将更新为对齐。

**注意： Windows 以前版本的 WaveCyclic 信息**

WaveCyclic 筛选器实现为端口/微型端口驱动程序对。 WaveCyclic 筛选器工厂创建 WaveCyclic 筛选器，如下所示：

-   它实例化 WaveCyclic 微型端口驱动程序对象。

-   它通过使用 GUID 值 **CLSID \_ PortWaveCyclic** 调用 [**PcNewPort**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)来实例化 WaveCyclic 端口驱动程序对象。

-   它调用端口驱动程序的 [**IPort：： Init**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init) 方法将微型端口驱动程序绑定到端口驱动程序。

[Subdevice 创建](subdevice-creation.md)中的代码示例演示了此过程。 端口和微型端口驱动程序通过其 [IPortWaveCyclic](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavecyclic) 和 [IMiniportWaveCyclic](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclic) 接口相互通信。

WaveCyclic 筛选器的循环缓冲区始终包含一个连续的虚拟内存块。 端口驱动程序的 [**IDmaChannel：： AllocateBuffer**](/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-allocatebuffer) 方法的实现始终分配一个在物理内存和虚拟内存地址空间中连续的缓冲区。 如前文所述，WaveCyclic 设备的 DMA 引擎对缓冲区内存施加了附加约束，微型端口驱动程序可以自由实现自己的缓冲区分配方法来满足这些约束。

一个 WaveCyclic 微型端口驱动程序，该驱动程序要求使用大的缓冲区 (例如，8个物理上连续的内存) 页，如果操作系统拒绝原始请求，则应准备好为更小的缓冲区大小。 有时可能会卸载和重新加载音频设备以便重新平衡系统资源 (参阅 [停止设备以重新平衡资源](../kernel/stopping-a-device-to-rebalance-resources.md)) 。

带有内置的总线主控 DMA 硬件的 WaveCyclic 设备称为 *主设备*。 或者，WaveCyclic 设备可以是无内置 DMA 硬件功能的 *从属设备* 。 从属设备必须依赖系统 DMA 控制器来执行所需的任何数据传输。 有关主设备和从属设备的详细信息，请参阅 [IDmaChannel](/windows-hardware/drivers/ddi/portcls/nn-portcls-idmachannel) and [IDmaChannelSlave](/windows-hardware/drivers/ddi/portcls/nn-portcls-idmachannelslave)。

WaveCyclic 微型端口驱动程序可以实现其自己的 DMA 通道对象，而不是使用默认 DMA 通道对象，该对象由端口驱动程序的新 *Xxx* DmaChannel 方法之一创建：

[**IPortWaveCyclic::NewMasterDmaChannel**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavecyclic-newmasterdmachannel)

[**IPortWaveCyclic::NewSlaveDmaChannel**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavecyclic-newslavedmachannel)

适配器驱动程序的自定义 [IDmaChannel](/windows-hardware/drivers/ddi/portcls/nn-portcls-idmachannel) 实现可以对数据执行自定义处理，以满足特殊的硬件限制。 例如，Windows 多媒体函数使用波形格式，其中16位样本始终为有符号值，但音频呈现硬件可能设计为使用不带符号的16位值。 在这种情况下，可以编写驱动程序的自定义 [**IDmaChannel：： CopyTo**](/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-copyto) 方法，将已签名的源值转换为硬件所需的无符号目标值。 尽管此方法可用于解决硬件设计缺陷，但它也会导致软件开销巨大的成本。

有关实现其自己的 DMA 通道对象的驱动程序的示例，请参阅 Sb16 的早期版本中的示例音频适配器。 如果将常量重 \_ 写 DMA \_ 通道定义为 **TRUE**，则源代码中的条件编译语句将启用专用的 [IDmaChannel](/windows-hardware/drivers/ddi/portcls/nn-portcls-idmachannel) 对象，驱动程序使用该对象替换 IPortWaveCyclic：： New *Xxx* DmaChannel 调用中的默认 IDmaChannel 对象。

 

