---
title: 开发 WaveRT 微型端口驱动程序
description: 开发 WaveRT 微型端口驱动程序
ms.date: 07/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f91de9821f751c5de74fb5c5a32884d589d9f36
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784871"
---
# <a name="developing-a-wavert-miniport-driver"></a>开发 WaveRT 微型端口驱动程序


本主题介绍在决定开发自己的 WaveRT 微型端口驱动程序时必须考虑的软件和硬件相关的要点。

Microsoft 制定了一套适用于 [通用音频体系结构 ](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/UAA_Guidelines.doc) 的硬件设计准则 (UAA) ，准则结合了我们建议用于 WaveRT 音频设备的功能。 UAA 准则与 Intel 开发 (HD) 音频规范的高清晰度密切相关。

Windows Vista 和更高版本的 Windows 操作系统为 UAA 兼容音频设备提供了 HD 音频驱动程序。 如果音频设备符合 UAA，则不必开发自己的 WaveRT 微型端口驱动程序。 但对于具有一些专有的非 UAA 硬件功能的音频设备，必须开发自己的 WaveRT 微型端口驱动程序来支持专用功能。

为了帮助你开发自己的 WaveRT 微型端口驱动程序，我们建议你先查看示例适配器驱动程序，然后查看 WaveRT 友好的 UAA 功能。

### <a name="span-idthe_sample_adapter_driverspanspan-idthe_sample_adapter_driverspanthe-sample-adapter-driver"></a><span id="the_sample_adapter_driver"></span><span id="THE_SAMPLE_ADAPTER_DRIVER"></span>示例适配器驱动程序

有关示例驱动程序的信息，请参阅 [示例音频驱动程序](sample-audio-drivers.md)。

### <a name="span-idthe_wavert_friendly_featuresspanspan-idthe_wavert_friendly_featuresspanthe-wavert-friendly-features"></a><span id="the_wavert_friendly_features"></span><span id="THE_WAVERT_FRIENDLY_FEATURES"></span>WaveRT 友好的功能

查看示例适配器驱动程序并开始设计 WaveRT 微型端口驱动程序之后，必须验证它是否支持以下软件和硬件功能。 因此，生成的微型端口驱动程序会与系统提供的 WaveRT 端口驱动程序和 Windows Vista [音频引擎](exploring-the-windows-vista-audio-engine.md)的操作模式兼容。

-   **低硬件延迟。** WaveRT 微型端口驱动程序必须提供 [**IMiniportWaveRTStream：： GetHWLatency**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertstream-gethwlatency) 方法的完全功能实现。 此方法对于支持 [**KSPROPERTY \_ RTAUDIO \_ HWLATENCY**](./ksproperty-rtaudio-hwlatency.md) 属性是必需的。

-   **FIFO 中断。** WaveRT 微型端口驱动程序必须在 FIFO 溢出和不足发生时自动生成中断。 当你在音频设备和驱动程序软件上运行测试时，此功能允许检测音频流中的故障。 如果没有硬件支持 (换言之，FIFO 中断) ，不存在用于获取问题信息的便利和可靠方法。

-   **散播-聚集 DMA 和缓冲区循环。** 当微型端口驱动程序支持具有分散收集功能的 DMA 控制器时，它允许将数据移入和移出循环缓冲，而无需通过微型端口驱动程序进行干预。

    当微型端口驱动程序支持可执行缓冲区循环的 DMA 控制器时，DMA 控制器可以在到达缓冲区末尾后，通过读取或写入操作自动换行到缓冲区的开头。 它可以执行环绕，无需通过微型端口驱动程序进行干预。

    请注意，WaveRT 端口驱动程序支持无法执行分散收集传输或自动缓冲区循环的现有硬件设计。

    如果音频设备缺少分散收集功能，则 WaveRT 微型端口驱动程序必须首先分配由内存中物理上连续的页组成的循环缓冲区。 然后，微型端口驱动程序使用 WaveRT 端口驱动程序中的 helper 函数来执行数据传输和自动缓冲区循环。 缺点是，由于系统的非分页内存池变得越来越多，请求分配大的连续物理内存块更有可能失败。 具有分散收集功能的设备不受内存碎片影响。

    如果当 DMA 通道到达循环缓冲的末尾时，音频设备无法自动执行缓冲区循环，则 WaveRT 微型端口驱动程序必须干预并配置通道，以开始在缓冲区开头传输数据。

-   **位置寄存器。** 对于新设计，硬件实施人员应为每个 DMA 通道包含位置寄存器。 位置寄存器将当前缓冲区位置指示为相对于循环缓冲区开始的字节偏移量。 位置寄存器读取在缓冲区的开头处为零。 当位置寄存器到达循环缓冲区的末尾时，它会自动换行到缓冲区的开头 (重置为零) 并随着缓冲区位置的向前继续递增。

    位置寄存器可以映射到虚拟内存，以便客户端可以直接读取寄存器。

    理想情况下，位置寄存器应指示当前通过数字到模拟和模拟到数字转换器进行移动的样本的缓冲区位置 (音频设备的 Dac 和 ADCs) 。

    但是，此信息可能不能直接从音频芯片提供，它将数字和模拟功能分割为单独的总线控制器和编码器/解码器 (编解码器) 芯片。 通常，位置寄存器位于总线控制器芯片中，每个寄存器指示控制器写入或读取编解码器的音频数据的位置。

    获取此类型的位置寄存器的读取后，客户端可以通过对编解码器添加或减去延迟来估算正在通过 Dac 或 ADCs 移动的样本的当前位置。 客户端从 **KSPROPERTY \_ RTAUDIO \_ HWLATENCY** 属性请求中获取编解码器延迟。 出于此原因，当端口驱动程序调用 **IMiniportWaveRTStream：： GetHardwareLatency** 方法以响应此类型的属性请求时，WaveRT 微型端口驱动程序必须准确地报告编解码器延迟。

    请注意，WaveRT 端口驱动程序支持缺少位置寄存器的现有硬件设计。 对于具有此限制的设备，WaveRT 微型端口驱动程序必须通过返回 " **\_ 不 \_ 受支持的状态**" 错误代码来调用 [**IMiniportWaveRTStream：： GetPositionRegister**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertstream-getpositionregister)方法，这会强制端口驱动程序对 [**KSPROPERTY \_ RTAUDIO \_ POSITIONREGISTER**](./ksproperty-rtaudio-positionregister.md)属性请求失败。 在这种情况下，客户端必须通过 [**KSPROPERTY \_ 音频 \_ 位置**](./ksproperty-audio-position.md) 属性获取当前位置，这会在每次读取位置导致用户模式和内核模式间转换的开销。

-   **时钟寄存器。** 时钟寄存器是 WaveRT 兼容音频设备的可选但有用的硬件功能。 音频应用程序可以使用时钟寄存器在两个或更多独立音频设备中同步音频流，这些设备具有不同且不同步的硬件时钟。 如果没有时钟寄存器，应用程序将无法检测硬件时钟之间的偏差并对其进行补偿。

    音频硬件用于通过数字到模拟或模拟到数字转换器来时钟音频数据的示例时钟应派生自时钟寄存器的内部时钟。 以异步方式对样本时钟进行增量递增的时钟寄存器不用于同步，不应公开。

    类似于位置寄存器，时钟寄存器可以映射到虚拟内存，以便客户端可以直接读取注册。

-   **音频处理对象。** 设计良好的 WaveRT 微型端口驱动程序决不能触摸音频设备的循环缓冲区中的音频数据。 应设计硬件，使音频数据直接在客户端和音频硬件之间流动，无需通过音频驱动程序软件进行干预。 但是，Windows Vista 支持两种类型的音频处理对象， (在不违反此规则的情况下执行软件处理音频数据的) ：

    -   LFX)  (的本地效果

        LFX 是执行一般音频处理功能 (例如，不特定于特定音频设备的均衡) 。 在将流添加到全局混合之前，LFX APO 会处理应用程序中的音频流。

    -   GFX)  (全局效果

        GFX 是对音频流执行特定于硬件的处理。 GFX APO 通过安装设备的 INF 文件绑定到特定音频设备。 GFX APO 的作用是全局性的，因为它会影响通过音频设备播放的全局混合。
    
    全局混合由音频引擎执行，音频引擎是负责混合来自所有音频应用程序的音频流的用户模式系统组件。 通常，音频引擎是通过循环缓冲区直接与 WaveRT 音频设备交换数据的客户端。

    当用户启用 LFX APO 时，音频系统会将 APO 插入到音频引擎的一个输入流中。 当用户启用 GFX APO 时，系统会将该 APO 从音频引擎插入到输出流中。 有关 LFX 和 GFX 的详细信息，请参阅 [探索 Windows Vista 音频引擎](exploring-the-windows-vista-audio-engine.md) 主题。

    仅可用于共享模式的音频流。 对于独占模式流，应用程序通过循环缓冲区直接与 WaveRT 硬件设备交换数据，而其他组件不能触摸缓冲中的数据。

 

