---
title: 开发 WaveRT 微型端口驱动程序
description: 开发 WaveRT 微型端口驱动程序
ms.assetid: d2d37c9e-fbfb-4bf3-bd7d-c8e19070a3f1
ms.date: 07/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 881105e63faa200ebcc09461a9ff8136f69f0402
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333807"
---
# <a name="developing-a-wavert-miniport-driver"></a>开发 WaveRT 微型端口驱动程序


本主题提供的软件和您决定开发您自己 WaveRT 微型端口驱动程序时必须考虑的与硬件相关的点。

Microsoft 已开发出一套硬件设计准则[通用音频体系结构 (UAA)](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/UAA_Guidelines.doc)和指导原则合并建议 WaveRT 音频设备的功能。 UAA 准则严格基于由 Intel 开发的高清晰度 (HD) 音频规范。

Windows Vista 和更高版本的 Windows 操作系统提供的 UAA 兼容的音频设备 HD 音频驱动程序。 因此如果 UAA 符合您的音频设备，你不必开发自己 WaveRT 微型端口驱动程序。 但对于某些专有，非 UAA 硬件功能的音频设备，必须开发自己的 WaveRT 微型端口驱动程序以支持的专有功能。

为了帮助您开发自己 WaveRT 微型端口驱动程序，我们建议首先查看示例适配器驱动程序，然后查看 WaveRT 友好 UAA 功能。

### <a name="span-idthesampleadapterdriverspanspan-idthesampleadapterdriverspanthe-sample-adapter-driver"></a><span id="the_sample_adapter_driver"></span><span id="THE_SAMPLE_ADAPTER_DRIVER"></span>示例适配器驱动程序

有关示例驱动程序的信息，请参阅[示例音频驱动程序](sample-audio-drivers.md)。

### <a name="span-idthewavertfriendlyfeaturesspanspan-idthewavertfriendlyfeaturesspanthe-wavert-friendly-features"></a><span id="the_wavert_friendly_features"></span><span id="THE_WAVERT_FRIENDLY_FEATURES"></span>WaveRT 友好的特性

查看示例适配器驱动程序并开始设计 WaveRT 微型端口驱动程序后，您必须验证它支持以下软件和硬件功能。 因此，然后生成该微型端口驱动程序将成为与系统提供 WaveRT 端口驱动程序和 Windows Vista 的操作模式兼容[音频引擎](exploring-the-windows-vista-audio-engine.md)。

-   **低的硬件的滞后时间。** WaveRT 微型端口驱动程序必须提供的全部功能的实现[ **IMiniportWaveRTStream::GetHWLatency** ](https://msdn.microsoft.com/library/windows/hardware/ff536747)方法。 此方法是可支持所需[ **KSPROPERTY\_RTAUDIO\_HWLATENCY** ](https://msdn.microsoft.com/library/windows/hardware/ff537378)属性。

-   **FIFO 中断。** WaveRT 微型端口驱动程序必须自动生成中断 FIFO 溢出和不足何时发生。 音频设备和驱动程序软件上运行测试时，此功能允许音频流中的故障检测。 如果没有硬件支持 （换而言之，FIFO 中断） 不方便、 可靠存在方法用于获取故障的信息。

-   **散播-聚集 DMA 和缓冲区循环。** 如果您的微型端口驱动程序支持具有散播-聚集的功能的 DMA 控制器，它允许数据移入和移出循环缓冲区而无需干预从微型端口驱动程序。

    时微型端口驱动程序支持 DMA 控制器可以执行缓冲区循环，DMA 控制器可以自动将回绕到的缓冲区开始后到达具有读取缓冲区的末尾或写操作。 它可以从您的微型端口驱动程序执行环绕而无需干预。

    请注意 WaveRT 端口驱动程序支持都不能在执行散播-聚集传输或自动缓冲区循环的现有硬件设计。

    如果音频设备缺少散播-聚集功能，WaveRT 微型端口驱动程序必须首先分配循环缓冲区在内存中物理上连续的页面组成。 微型端口驱动程序然后使用 helper 函数在 WaveRT 端口驱动程序中执行数据传输和自动缓冲区循环。 缺点是系统的，随着越来越多地形成碎片非分页的内存池，分配的连续的物理内存的大块的请求是系统的更有可能会失败。 散播-聚集功能的设备不受内存碎片。

    DMA 通道达到循环缓冲区的末尾时，将音频设备不能自动执行缓冲区循环，如果 WaveRT 微型端口驱动程序必须介入并配置通道开始的缓冲区开始处的数据传输。

-   **位置注册。** 新设计的硬件实现程序应包括每个 DMA 通道位置注册。 位置注册指示当前缓冲区的字节偏移量从一开始为循环缓冲区的位置。 读取位置注册为零的缓冲区开始处。 当位置注册达到循环缓冲区的末尾时，它会自动将绕回到缓冲区 （重置为零） 的开头和仍将继续作为缓冲区位置前移的递增。

    位置寄存器可以映射到的虚拟内存，以便客户端可以直接读取寄存器。

    理想情况下，位置寄存器应指示了通过数字模拟和模拟到数字转换器 （Dac 和 ADCs） 的音频设备的当前移动的示例的缓冲区位置。

    但是，此信息可能不能直接从数字和模拟功能划分为单独的总线控制器和编码器/解码器 （编码解码器） 的芯片音频芯片集。 通常情况下，位置寄存器位于总线控制器芯片，并且每个注册指示控制器是写入还是读取编解码器的音频数据的位置。

    从这种类型的位置获取读取后注册、 客户端可以估计的示例通过 Dac 或 ADCs 通过增加或减少通过编解码器的延迟要移动的当前位置。 客户端获取从的编解码器延迟**KSPROPERTY\_RTAUDIO\_HWLATENCY**属性请求。 出于此原因，WaveRT 微型端口驱动程序必须准确地报告的编解码器延迟时端口驱动程序调用**IMiniportWaveRTStream::GetHardwareLatency**方法以这种类型的属性请求的响应。

    请注意 WaveRT 端口驱动程序支持现有的硬件设计缺少位置寄存器的。 WaveRT 微型端口驱动程序必须具有此限制的设备，故障对调用[ **IMiniportWaveRTStream::GetPositionRegister** ](https://msdn.microsoft.com/library/windows/hardware/ff536752)方法通过返回**状态\_不\_支持**错误代码，这会强制端口驱动程序故障[ **KSPROPERTY\_RTAUDIO\_POSITIONREGISTER** ](https://msdn.microsoft.com/library/windows/hardware/ff537381)属性的请求。 在这种情况下，客户端必须获取通过当前位置[ **KSPROPERTY\_音频\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff537297)属性，这会导致用户模式之间的转换的开销和内核模式下，每个位置读取。

-   **时钟寄存器。** 时钟注册是可选的但有用的硬件功能 WaveRT 兼容音频设备。 音频应用程序可以使用时钟注册同步在两个或多个独立音频设备具有单独的和不同步硬件时钟的音频流。 而无需时钟寄存器中，应用程序是无法检测和补偿之间的硬件时钟偏差。

    音频硬件使用时钟通过数字模拟或模拟到数字转换器的音频数据的示例时钟应派生自递增的时钟寄存器的内部时钟。 时钟寄存器是异步示例时钟方面的速率递增属于同步不使用，不应公开。

    类似于位置寄存器，时钟注册可以映射到的虚拟内存，以便客户端可以直接读取注册。

-   **音频处理对象。** 设计良好的 WaveRT 微型端口驱动程序必须永远不会涉及将音频设备循环缓冲区中的音频数据。 硬件应由进行设计，以便直接之间的客户端和音频硬件而无需干预的音频数据流动的音频驱动程序软件。 但是，Windows Vista 支持两种类型的执行软件处理的音频数据，而不违反此规则的音频处理对象 (Apo):

    -   本地效果 (LFX) a p o s

        LFX 不执行并不特定于特定的音频设备的通用音频处理功能 （例如，均衡）。 LFX APO 流添加到全局组合之前处理从应用程序的音频流。

    -   全局效果 (GFX) a p o s

        GFX 不执行特定于硬件的处理的音频流。 GFX APO 绑定到特定的音频设备，通过安装设备的 INF 文件。 GFX APO 的效果是全局的因为它会影响所播放的音频设备的全局组合。
    
    是用户模式系统组件，它负责从所有音频的应用程序的音频流混合为音频引擎执行全局混合使用。 通常情况下，此音频引擎是直接与通过循环缓冲区 WaveRT 音频设备交换数据的客户端。

    当用户启用 LFX APO 时，音频系统将 APO 插入到其中一个输入流到音频引擎。 当用户启用 GFX APO 时，系统会将该 APO 插入到输出流从音频引擎。 有关 LFX 和 GFX a p o s 和音频引擎的详细信息，请参阅[探究 Windows Vista 音频引擎](exploring-the-windows-vista-audio-engine.md)主题。

    不是只适用于共享模式音频流可用。 排他模式流的应用程序直接与 WaveRT 硬件设备的整个循环缓冲区，交换数据和任何其他组件可以触摸的缓冲区中的数据。

 

 




