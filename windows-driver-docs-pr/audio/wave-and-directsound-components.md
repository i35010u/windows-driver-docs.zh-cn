---
title: Wave 和 DirectSound 组件
description: Wave 和 DirectSound 组件
ms.assetid: df00fcaf-49b0-4af1-a12f-bd3fcb9e025d
keywords:
- 批组件 WDK 音频
- 批流 WDK 音频
- DirectSound WDK 音频，组件
- 用户模式组件 WDK 音频
- 内核模式组件 WDK 音频
- 批呈现 WDK 音频
- 批捕获 WDK 音频
- 呈现组件 WDK 音频
- 捕获组件 WDK 音频
- 批呈现应用程序 WDK 音频
- 批捕获应用程序 WDK 音频
- 批扩展的应用程序 WDK 音频
- 批中的应用程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2acbfc84da63ea183c31742ee8a0a3b108824356
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328511"
---
# <a name="wave-and-directsound-components"></a>Wave 和 DirectSound 组件


## <span id="wave_and_directsound_components"></span><span id="WAVE_AND_DIRECTSOUND_COMPONENTS"></span>


应用程序的程序依赖于用户模式和内核模式下捕获 （输入） 和呈现 （输出） 批流的组件的组合。 批流是由描述其数据格式的数字音频流[ **WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff538799)或[ **WAVEFORMATEXTENSIBLE** ](https://msdn.microsoft.com/library/windows/hardware/ff538802)结构。

应用程序可以使用以下任一批呈现和捕获的软件接口：

-   Microsoft Windows 多媒体 waveOut*Xxx*和 waveIn*Xxx*函数

-   DirectSound 和 DirectSoundCapture Api

行为的 waveOut*Xxx*和 waveIn*Xxx*函数基于旧批驱动程序和设备的功能。 从 Windows 98 [WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)对这些函数的调用转换为与 WDM 音频驱动程序的命令。 但是，通过模拟行为的旧版软件和硬件、 waveOut*Xxx*三维声音效果和，现可通过 DirectSound API 的硬件加速，否则会影响函数。 有关 DirectSound 和 Windows 多媒体批函数的详细信息，请参阅 Microsoft Windows SDK 文档。

DirectSound 和 Windows 多媒体批函数都的客户端[SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)，哪些生成处理批和 DirectSound 流音频筛选器关系图。 图形构建是透明的使用这些软件接口的应用程序。

### <a name="span-idwavecomponentsspanspan-idwavecomponentsspanspan-idwavecomponentsspanwave-components"></a><span id="Wave_Components"></span><span id="wave_components"></span><span id="WAVE_COMPONENTS"></span>批组件

下图显示了用户模式和内核模式组件批应用程序用来呈现或捕获包含批 PCM 数据的数字音频流。

![说明批呈现和捕获组件的关系图](images/wavecomp.png)

呈现组件显示在上图中，左侧和右侧显示捕获组件。 表示批微型端口驱动程序的框会变暗，以指示这些是供应商提供的组件。 在图中的其他组件是系统提供。

在左上角的图、 批呈现 （或"批扩展"） 的应用程序接口到 WDM 音频驱动程序通过 waveOut*Xxx*函数，在用户模式下实现[WinMM 系统组件](user-mode-wdm-audio-components.md#winmm_system_component)，Winmm.dll。 应用程序从一个文件并调用读取块波形音频示例[ **waveOutWrite** ](https://msdn.microsoft.com/library/windows/desktop/dd743876)函数来呈现它们。

WDMAud，其中包含用户模式和内核模式组件 （Wdmaud.drv 和 Wdmaud.sys），缓冲批数据从[ **waveOutWrite** ](https://msdn.microsoft.com/library/windows/desktop/dd743876)调用，并输出到波形流[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)，其显示下方 WDMAud 图中。

KMixer 是接收的批 PCM 流从一个或多个源和混合使用它们一起以形成单个输出流，在 wave PCM 格式中也是一个系统组件。

KMixer 输出批流到 WaveCyclic 或 WavePci 设备时，其端口和微型端口驱动程序将出现在上图中左侧 KMixer 的下方。 微型端口驱动程序将自身绑定到端口驱动程序，以形成批筛选器表示基础音频呈现设备。 典型的渲染设备输出驱动器扬声器或外部的音频单元的一组模拟信号。 渲染设备也可能会输出通过 S/PDIF 连接器的数字音频。 有关 WaveCyclic 和 WavePci 的详细信息，请参阅[批筛选器](wave-filters.md)。

或者，KMixer 可以到 USB 音频设备，通过控制传递的输出流[USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)（未在图中显示），而不是 WaveCyclic 或 WavePci 设备。

适配器驱动程序通过调用创建 WaveCyclic 或 WavePci 端口驱动程序的实例[ **PcNewPort** ](https://msdn.microsoft.com/library/windows/hardware/ff537715) GUID 值为**CLSID\_PortWaveCyclic**或**CLSID\_PortWavePci**分别。

上图右侧显示了支持捕获到文件的波形数据的应用程序所需的组件。 批捕获 （或"批中"） 应用程序与 WDM 音频驱动程序通过 waveIn*Xxx* WinMM 系统组件中实现的函数。

在该图的右下角，批捕获设备受批微型端口和端口驱动程序。 端口和微型端口驱动程序，它可以是类型 WaveCyclic 或 WavePci，一起绑定到窗体表示捕获设备的批筛选器。 此设备通常捕获从麦克风或其他音频源的模拟信号并将其转换为批 PCM 流。 设备还可能会输入通过 S/PDIF 连接器的数字音频流。

波形端口驱动程序直接输出到 KMixer 或 WDMAud 其批流。 如果它必须是采样率转换之前 WDMAud 接收流必须经过 KMixer。 执行同时呈现和捕获音频流的系统可能需要 KMixer，两个的实例，如图所示。 请注意 SysAudio 会自动创建这些实例，因为需要它们。

或者，而不是 WaveCyclic USB 音频设备或 WavePci 设备可以是捕获的批流的源。 在这种情况下，USBAudio 驱动程序 （不在图中所示） 将流传递到 KMixer。

无论是否通过 USB 设备或 WaveCyclic 或 WavePci 设备捕获批流，KMixer 执行采样率转换流，如果需要而不会与其他流没有混合。 KMixer 输出到 Wdmaud.sys，内核模式下生成的流一半 WDMAud 系统驱动程序。 用户模式 Wdmaud.drv，一半时，输出批流式传输到应用程序通过 waveIn*Xxx*函数，这在 Winmm.dll 中实现。 最后，在图顶部，批捕获应用程序将批数据写入文件。

在批捕获应用程序调用的时间[ **waveInOpen** ](https://msdn.microsoft.com/library/windows/desktop/dd743847)函数打开捕获流，它会传入一个指针，到其回调例程。 批捕获事件发生时，操作系统将使用包含波样本的捕获设备从下一个块的缓冲区调用回调例程。 回调响应，该应用程序的下一批数据块写入文件。

### <a name="span-iddirectsoundcomponentsspanspan-iddirectsoundcomponentsspanspan-iddirectsoundcomponentsspandirectsound-components"></a><span id="DirectSound_Components"></span><span id="directsound_components"></span><span id="DIRECTSOUND_COMPONENTS"></span>DirectSound 组件

下图显示了 DirectSound 应用程序使用呈现或捕获批数据的用户模式和内核模式组件。

![说明 directsound 呈现和捕获组件的关系图](images/dscomp.png)

在上图中的左半部分显示了呈现的组件和捕获组件显示在右侧。 批微型端口驱动程序显示为变暗的框，以指示它们是供应商提供的组件。 在图中的其他组件是系统提供。

在左上角的图、 DirectSound 应用程序加载批文件中的数据与声音缓冲用户模式[DirectSound 系统组件](user-mode-wdm-audio-components.md#directsound_system_component)(Dsound.dll) 管理。 此组件将批流发送到 WaveCyclic 或 WavePci 设备，其端口和微型端口驱动程序显示在图中，左下角。 如果设备上的可用硬件 mixer pin，流将直接向波形端口驱动程序，从而绕过 KMixer 传递。 否则，该流首先通过 KMixer，包含与任何其他同时播放流传递。 KMixer 输出混合流式传输到端口驱动程序。

作为前，微型端口驱动程序将绑定本身到端口驱动程序，以形成批筛选器表示基础音频呈现设备。 此设备可能例如播放通过扬声器，一组流。

或者，可以通过 USB 音频设备，而不是 WaveCyclic 或 WavePci 设备呈现批流。 在这种情况下，该流不能绕过 KMixer;（图中未显示） 的 USBAudio 类系统驱动程序始终将流传递到 KMixer。

上图右侧显示了支持 DirectSoundCapture 应用程序的组件。 是在应用程序记录批数据接收从 WaveCyclic 或 WavePci 捕获设备。 此设备将转换模拟信号从麦克风，例如，为批流。 设备的波形端口和微型端口驱动程序将显示在图右下角。 如图所示，端口驱动程序接收作为输入流从微型端口驱动程序，并将其输出到的用户模式下 DirectSound 组件 Dsound.dll，直接或通过 KMixer 间接。 这取决于硬件捕获 pin 是否可从捕获设备。

或者，捕获的批流的源可以是 USB 音频设备。 在这种情况下，该流不能绕过 KMixer;（图中未显示） 的 USBAudio 驱动程序始终将流传递到 KMixer。

如果 KMixer 插入到捕获流的路径，它在流上执行采样率转换，如有需要而不是与其他流没有混合。

在上图中的右上角，应用程序从 DirectSoundCapture 缓冲区中读取的波形数据，并将其写入文件。

 

 




