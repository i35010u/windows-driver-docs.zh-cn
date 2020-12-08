---
title: WavePci 延迟
description: WavePci 延迟
keywords:
- WavePci 延迟 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e292009b5fcceffb49aa0b7e1a4a1f562b4cf41
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798793"
---
# <a name="wavepci-latency"></a>WavePci 延迟


## <span id="wavepci_latency"></span><span id="WAVEPCI_LATENCY"></span>


WavePci 端口驱动程序以不同于 WaveCyclic 驱动程序的方式处理音频流的缓冲。

如果你的 WavePci 微型端口驱动程序提供硬件混合，则 DirectSound 会将 IRP 提交到 WavePci 端口驱动程序，该驱动程序包含一个循环缓冲区中的整个 DirectSound 波形流。 DirectSound 将缓冲区分配为虚拟内存的连续块。 为了避免复制 DirectSound 缓冲区，内核流式处理层会将缓冲区映射到内核模式虚拟内存，并生成 MDL (内存描述符列表) ，该列表指定了循环缓冲区中内存页的虚拟地址和物理地址。 WavePci 端口驱动程序将循环缓冲区分区为分配器帧序列 (参见 [KS 分配器](../stream/ks-allocators.md)) 。 当端口驱动程序在流初始化期间调用其 [**IMiniportWavePciStream：： GetAllocatorFraming**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-getallocatorframing) 方法时，微型端口驱动程序指定其首选分配器帧大小。 但是，SysAudio （系统图形生成器）可以覆盖微型端口驱动程序的首选项，以便满足音频筛选器图中其他组件的要求。

WavePci 端口驱动程序将循环缓冲作为一系列映射公开给微型端口驱动程序。 映射可以是整个分配帧或帧的一部分。 如果特定的分配帧完全位于某个页面内，则端口驱动程序会将该帧作为单个映射提供给微型端口驱动程序。 如果分配帧跨越一个或多个页面边界，则端口驱动程序将在每个页面边界处拆分该帧，并将其显示为两个或多个映射。 对 [**IPortWavePciStream：： GetMapping**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-getmapping) 的每个调用都会生成序列中的下一个后续映射。

与 WaveCyclic 大小写相比，在这种情况下，微型端口驱动程序对在硬件上缓冲的数据量有很大的控制，WavePci 微型端口驱动程序对它在任何时间都已打开的映射数量有相当大的控制权。 每次调用 [**GetMapping**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-getmapping) 时，打开的映射数增加1，并在每次调用 [**ReleaseMapping**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-releasemapping)时减少一次。 当然， (**GetMapping** 调用可能会失败，因此，驱动程序不会控制对映射数量的控制。 ) 通过控制打开的映射的数目并跟踪映射的累计大小，微型端口驱动程序可以在依赖于映射) 大小的公差范围内确定 (可用于硬件的缓冲的毫秒数。 你的 WavePci 微型端口驱动程序应该请求足够的页映射，以降低到可接受级别的几率。

如果微型端口驱动程序的策略是缓冲最多50毫秒的数据（例如，在读取和写入指针之间），请记住，此限制表示你的驱动程序将累积的最大数据量，但它不能表示驱动程序对流延迟的贡献。 应将驱动程序设计为尽可能小地保持其延迟。 当微型端口驱动程序在开始播放新流之前获取其初始映射集时，微型端口驱动程序可以继续请求映射，直到它达到其缓冲区限制（在此) 示例中为50毫秒） (毫秒，或者不再有可用的映射。 但在后一种情况下，微型端口驱动程序不得等待，直到有更多映射可用，然后才能开始播放流。 相反，驱动程序应立即开始播放已获得的映射。 以后，当有更多的映射可用时，驱动程序可以继续获取更多映射，直到它达到其缓冲区大小限制，或者不再有更多的映射可立即使用。

通常，WavePci 设备的 DMA 硬件应设计为直接访问以任意字节对齐方式存储的音频帧，并在物理内存的非连续页面之间跨边界。 如果你的设备需要映射为整数个音频帧数量，则该设备受其支持的各种音频格式的限制。 当然，具有此限制的设备还应能够处理两个的音频帧大小。

例如，具有四个通道和16位样本大小的设备需要8字节的音频帧大小。 整数数量的音频帧适用于一页 (或任意其他分配帧大小，该大小是八个字节的倍数) 。 但是，对于带有16位样本的5.1 通道流，音频帧大小为12个字节，超过单个页面大小的流一定包含跨页面边界的音频帧。  ([波形筛选器](wave-filters.md) 中的图说明了此问题。 ) 无法处理任意字节对齐和任意字节长度映射的硬件必须依赖于驱动程序来执行中间复制，这会降低性能。

 (WDK) 的 Microsoft Windows 驱动程序工具包中的 Ac97 示例适配器驱动程序实现 [**GetAllocatorFraming**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-getallocatorframing) 方法。 微型端口驱动程序使用此方法来传达其首选的帧分配大小。 在 Windows 2000 和 Windows Me 中，仅当 [拆分器系统驱动程序](kernel-mode-wdm-audio-components.md#splitter_system_driver) ( # A0) 在输出 pin 上方实例化时，端口驱动程序才会调用此方法。 在 Windows XP 和更高版本中，端口驱动程序也为输入流调用此方法。 请记住，当决定帧分配大小时，SysAudio 可能会选择忽略微型端口驱动程序的首选项。

 

