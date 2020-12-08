---
title: Wave 和 DirectSound 组件
description: Wave 和 DirectSound 组件
keywords:
- 波形组件 WDK 音频
- 波形流 WDK 音频
- DirectSound WDK 音频，组件
- 用户模式组件 WDK 音频
- 内核模式组件 WDK 音频
- 波形渲染 WDK 音频
- 波形捕获 WDK 音频
- 呈现组件 WDK 音频
- 捕获组件 WDK 音频
- 波形渲染应用程序 WDK 音频
- 波形捕获应用程序 WDK 音频
- wave out 应用程序 WDK 音频
- 波形应用程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4e8ca25b83c2ea0df3c3f2f5cd2093de4193b72
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800437"
---
# <a name="wave-and-directsound-components"></a>Wave 和 DirectSound 组件


## <span id="wave_and_directsound_components"></span><span id="WAVE_AND_DIRECTSOUND_COMPONENTS"></span>


应用程序依赖于用户模式和内核模式组件的组合来捕获 (输入) 并呈现 (输出) 波形流。 波形流是一种数字音频流，其数据格式由 [**WAVEFORMATEX**](/windows/win32/api/mmeapi/ns-mmeapi-waveformatex) 或 [**WAVEFORMATEXTENSIBLE**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible) 结构描述。

应用程序可以使用以下任一软件接口进行波形渲染和捕获：

-   Microsoft Windows 多媒体 waveOut *xxx* 和 waveIn *Xxx* 函数

-   DirectSound 和 DirectSoundCapture Api

WaveOut *xxx* 和 waveIn *xxx* 函数的行为基于旧式 wave 驱动程序和设备的功能。 从 Windows 98 开始， [WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver) 将对这些函数的调用转换为 WDM 音频驱动程序的命令。 但是，通过模拟旧软件和硬件的行为，waveOut *Xxx* 函数会牺牲现在通过 DirectSound API 提供的3-d 声音效果和硬件加速。 有关 DirectSound 和 Windows 多媒体波形函数的详细信息，请参阅 Microsoft Windows SDK 文档。

DirectSound 和 Windows 多媒体波形函数是 [SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)的客户端，它可生成用于处理 Wave 和 DirectSound 流的音频筛选器图形。 图形构建对于使用这些软件接口的应用程序而言是透明的。

### <a name="span-idwave_componentsspanspan-idwave_componentsspanspan-idwave_componentsspanwave-components"></a><span id="Wave_Components"></span><span id="wave_components"></span><span id="WAVE_COMPONENTS"></span>波形组件

下图显示了一个用户模式和内核模式组件，wave 应用程序使用这些组件来呈现或捕获由波形 PCM 数据组成的数字音频流。

![阐释波形渲染和捕获组件的示意图](images/wavecomp.png)

呈现组件显示在上图的左侧，而捕获组件显示在右侧。 表示波形微型端口驱动程序的框变暗，表示这些是供应商提供的组件。 图形中的其他组件是系统提供的。

在图的左上角，波形渲染 (或 "向外" ) 应用程序通过 waveOut *Xxx* 函数（在用户模式 [winmm.dll 系统组件](user-mode-wdm-audio-components.md#winmm_system_component)中实现，Winmm.dll）与 WDM 音频驱动程序进行接口。 应用程序从文件中读取波形音频样本块，并调用 [**waveOutWrite**](/previous-versions/dd743876(v=vs.85)) 函数进行呈现。

WDMAud，它包括用户模式和内核模式组件 (winspool.drv 和 Wdmaud.sys) ，将波形数据从 [**waveOutWrite**](/previous-versions/dd743876(v=vs.85)) 调用中缓冲，并将波形流输出到 [KMixer 系统驱动程序，该驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)将显示在图中的 WDMAud 下方。

KMixer 是一种系统组件，用于接收来自一个或多个源的声波 PCM 流，并将它们组合在一起以形成单个输出流（也采用波形 PCM 格式）。

KMixer 会将波形流输出到 WaveCyclic 或 WavePci 设备，其端口和微型端口驱动程序显示在上图左侧 KMixer 的下方。 微型端口驱动程序将自身绑定到端口驱动程序，以形成表示基础音频呈现设备的波形筛选器。 典型的渲染设备输出模拟信号，该信号用于驱动一组扬声器或外部音频装置。 呈现设备还可以通过 S/PDIF 连接器输出数字音频。 有关 WaveCyclic 和 WavePci 的详细信息，请参阅 [波形筛选器](wave-filters.md)。

或者，KMixer 可以将其输出流传递到 USB 音频设备，该设备由 [USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver) 控制 (不显示在图) 中，而不是 WaveCyclic 或 WavePci 设备。

适配器驱动程序通过分别调用带有 **CLSID \_ PortWaveCyclic** 或 **clsid \_ PortWavePci** 的 GUID 值的 [**PcNewPort**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport) ，创建 WaveCyclic 或 WavePci 端口驱动程序的实例。

上图的右侧显示了支持向文件捕获波形数据的应用程序所需的组件。 波形捕获 (或 "wave" ) 应用程序通过 waveIn *Xxx* 函数与 WDM 音频驱动程序通信，这些函数在 winmm.dll 系统组件中实现。

在该图的右下角，波形捕获设备由波形微型端口和端口驱动程序控制。 端口和微型端口驱动程序（可以是 WaveCyclic 或 WavePci 类型）将绑定在一起以形成表示捕获设备的波形筛选器。 此设备通常从麦克风或其他音频源捕获模拟信号，并将其转换为波形 PCM 流。 设备还可以通过 S/PDIF 连接器输入数字音频流。

波形端口驱动程序将其波形流输出到 KMixer 或直接 WDMAud。 如果流在 WDMAud 接收它之前需要进行采样速率转换，则必须通过 KMixer。 执行音频流的同时呈现和捕获的系统可能需要 KMixer 的两个实例，如图中所示。 请注意，SysAudio 会根据需要自动创建这些实例。

或者，捕获的波形流的源可以是 USB 音频设备，而不是 WaveCyclic 或 WavePci 设备。 在这种情况下，USBAudio 驱动程序 (未在图中显示) 将流传递到 KMixer。

无论波形流是由 USB 设备还是由 WaveCyclic 或 WavePci 设备捕获，KMixer 在流上执行采样率转换（如果需要），但不与其他流混合使用。 KMixer 会将生成的流输出到 Wdmaud.sys （WDMAud 系统驱动程序的内核模式）。 用户模式半 Wdmaud，winspool.drv 通过 waveIn *Xxx* 函数（在 Winmm.dll 中实现）将波形流输出到应用程序。 最后，在图的顶部，波形捕获应用程序会将波形数据写入文件。

当波形捕获应用程序调用 [**waveInOpen**](/previous-versions/dd743847(v=vs.85)) 函数来打开捕获流时，它将传入指向其回调例程的指针。 发生波形捕获事件时，操作系统将调用带有缓冲区的回调例程，该缓冲区包含捕获设备中的下一个波形样本块。 在响应回调时，应用程序会将下一个波形数据块写入文件。

### <a name="span-iddirectsound_componentsspanspan-iddirectsound_componentsspanspan-iddirectsound_componentsspandirectsound-components"></a><span id="DirectSound_Components"></span><span id="directsound_components"></span><span id="DIRECTSOUND_COMPONENTS"></span>DirectSound 组件

下图显示了 DirectSound 应用程序用来呈现或捕获波数据的用户模式和内核模式组件。

![说明 directsound 渲染和捕获组件的示意图](images/dscomp.png)

呈现组件显示在上图的左半部分，而捕获组件显示在右侧。 波形微型端口驱动程序显示为暗盒，指示它们是供应商提供的组件。 图形中的其他组件是系统提供的。

在图的左上角，DirectSound 应用程序将文件中的波形数据加载到用户模式 [DirectSound 系统组件](user-mode-wdm-audio-components.md#directsound_system_component) ( # A0) 管理的声音缓冲区。 此组件向 WaveCyclic 或 WavePci 设备发送一个波形流，其端口和微型端口驱动程序显示在图的左下方。 如果设备上有硬件合成器 pin，则会绕过 KMixer，将流直接传递到波形端口驱动程序。 否则，流首先传递 KMixer，这会将它与任何其他同时播放的流混合使用。 KMixer 将混合流输出到端口驱动程序。

与之前一样，微型端口驱动程序将自身绑定到端口驱动程序以形成表示基础音频呈现设备的波形筛选器。 例如，此设备可以通过一组扬声器播放流。

或者，可以通过 USB 音频设备而不是 WaveCyclic 或 WavePci 设备呈现波形流。 在这种情况下，流不能跳过 KMixer;图) 中未显示 USBAudio 类系统驱动程序 (始终将流传递到 KMixer。

上图的右侧显示了支持 DirectSoundCapture 应用程序的组件。 应用程序记录从 WaveCyclic 或 WavePci 捕获设备接收到的波形数据。 此设备将模拟信号从麦克风（例如）转换为波形流。 设备的波形端口和微型端口驱动程序显示在图的右下角。 如图所示，端口驱动程序接收来自微型端口驱动程序的流并将其直接输出到用户模式 DirectSound 组件、Dsound.dll 或通过 KMixer 间接输出。 这取决于是否可从捕获设备获取硬件捕获 pin。

或者，捕获的波形流的源可以是 USB 音频设备。 在这种情况下，流不能跳过 KMixer;图) 中未显示 USBAudio 驱动程序 (始终将流传递到 KMixer。

如果 KMixer 插入到捕获流的路径中，则它会根据需要在流上执行采样速率转换，但不会与其他流混合。

在上图的右上角，应用程序从 DirectSoundCapture 缓冲区读取波形数据并将其写入文件。

 

