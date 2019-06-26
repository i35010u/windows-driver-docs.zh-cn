---
title: 音频处理对象体系结构
description: 音频处理对象 (Apo) 提供 Windows 音频流的可自定义软件基于数字信号处理。
ms.assetid: 2F57B4C7-8C83-4DDF-BFAF-B9308752E91D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2c66e12c6f59e59a06bf486a26bf97a3fe98697
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355677"
---
# <a name="audio-processing-object-architecture"></a>音频处理对象体系结构


音频处理对象 (Apo) 提供 Windows 音频流的可自定义软件基于数字信号处理。

## <a name="span-idaudioprocessingobjectsoverviewspanspan-idaudioprocessingobjectsoverviewspanspan-idaudioprocessingobjectsoverviewspanaudio-processing-objects-overview"></a><span id="Audio_Processing_Objects_Overview"></span><span id="audio_processing_objects_overview"></span><span id="AUDIO_PROCESSING_OBJECTS_OVERVIEW"></span>音频处理对象概述


Windows 允许 Oem 和第三方音频硬件制造商许多增值功能，其音频驱动程序中包含自定义数字信号处理效果。 这些效果打包为用户模式系统效果音频处理对象 (Apo)。

音频处理对象 (Apo) 提供 Windows 音频流的软件基于数字信号处理。 APO 是 COM 主机对象，包含一种算法，旨在提供特定的数字信号处理 (DSP) 效果。 此功能是非正式地称为"音频效果"。 示例不包括图形均衡器、 混响、 震音，声学回声抵消 (AEC) 和自动增益控制 (AGC)。 不是基于 COM 的、 实时和进程内的对象。

**请注意**  的说明和本文档中的术语是指主要输出设备。 但是，技术是对称的并且工作实质上是按相反的顺序输入设备。

 

**软件未 vs。硬件 DSP**

硬件数字信号处理器 (DSP) 是专用的微处理器 （或 SIP 块），与针对操作需求的数字信号处理优化其体系结构。 可以有明显的优点与使用软件 APO 的专门构建硬件中实现音频处理。 一个优点是使用 cpu 资源和关联的功率消耗可能会较低的硬件实现 DSP。

想要实现一种软件之前，请考虑约束基于 APO 和一些其他优点和缺点，还需要考虑特定于的你项目的目标。

基于软件的效果会插入流初始化上的软件设备管道中。 这些解决方案执行所有处理主 CPU 上其效果并不依赖于外部硬件。 驱动程序和硬件仅支持原始处理时，此类型是解决方案的最佳 HDAudio、 USB 和蓝牙设备等传统 Windows 音频解决方案。 有关原始数据处理的详细信息，请参阅[音频信号处理模式](audio-signal-processing-modes.md)。

**代理 APO 硬件 DSP**

在硬件中 DSP 需要通过代理 APO 播发应用任何效果。 Microsoft 提供的默认代理 APO (MsApoFxProxy.dll)。 若要使用 Microsoft 提供的 APO，此属性和属性必须支持。

-   [KSPROPSETID\_AudioEffectsDiscovery](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-audioeffectsdiscovery)
-   [KSPROPERTY\_AUDIOEFFECTSDISCOVERY\_EFFECTSLIST](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn457706(v=vs.85))

（可选） 可以实现自己的代理 APO。

**Windows 提供 （系统） 不**

Windows 安装一组默认的 a p o s，提供了许多不同的音频效果。 有关系统的列表提供 APO 效果，请参阅[音频信号处理模式](audio-signal-processing-modes.md)。

Oem 可以包括所有系统提供不或替换自定义不为某些或所有规则。

**自定义 a p o s**

可以创建自定义不以通过添加其他音频效果增强 Windows 音频体验它。

它们提供 Windows 时，OEM 可以包括提供的 Windows a p o s 和自定义 a p o s 的任意组合。

自定义 APO 可以由 OEM 或第三方来增强音频体验已购买设备后安装。 当用户通过使用标准的 INF 文件安装的音频设备驱动程序时，它们会自动有权访问系统的 a p o s。 独立硬件供应商 (Ihv) 和原始设备制造商 (Oem) 可以同时仍可使用 Microsoft 类驱动程序提供其他自定义系统效果。 此，它们打包不作为其 DSP 算法和修改标准的 INF 文件，将其未插入音频引擎的信号处理关系图。

有关详细信息创建自定义不，请参阅[实现音频处理对象](implementing-audio-processing-objects.md)。

**自定义 APO 属性用户界面**

在台式计算机，可以创建自定义的 APO 属性页，以允许用户配置自定义 APO 与关联的设置。 此自定义 APO 页可为用户作为标准的 Windows 音频设置的扩展。

SYSVAD 音频示例包含一个示例自定义 APO 控件示例。 此屏幕截图显示了 SYSVAD 音频交换 APO 示例的属性页。

![sysvad 音频交换 apo 控件示例的演讲者属性页的屏幕截图](images/audio-apo-speaker-properties.png)

添加 APO 的详细信息对话框面板，请参阅[对于配置 APO 效果实现 UI](implementing-a-ui-for-configuring-apo-effects.md)。

**自定义 APO 测试和要求**

Microsoft HLK 提供了可用于不的测试。 有关音频测试，请参阅详细信息[Device.Audio 测试](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj123955(v=vs.85))并[Device.Audio 测试](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124726(v=vs.85))。

不使用时，这两个测试可以是特别有用。

[验证音频 EffectsDiscovery （手动） 的证书](https://docs.microsoft.com/previous-versions/windows/hardware/hck/dn456312(v=vs.85))

[SysFX 测试](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124017(v=vs.85))

有关音频支持不要求的信息，请参阅[Device.Audio 要求](https://docs.microsoft.com/previous-versions/windows/hardware/cert-program/deviceaudio-requirements)。

**自定义 APO 工具和实用程序**

"音频效果发现示例"可用于浏览可用的音频效果。 此示例演示如何查询上呈现音频效果和捕获音频设备以及如何使用音频效果监视更改。 它是 SDK 示例的一部分，可使用此链接下载：

[音频效果发现示例](https://code.msdn.microsoft.com/windowsapps/Audio-effects-discovery-5fd65c15)

**应用程序音频效果意识**

应用程序具有调用 Api，以确定哪些音频效果是在系统上当前处于活动状态的能力。 有关音频效果感知 Api 的详细信息，请参阅[AudioRenderEffectsManager 类](https://docs.microsoft.com/uwp/api/Windows.Media.Effects.AudioRenderEffectsManager)。

## <a name="span-idaudioprocessingobjectsarchitecturespanspan-idaudioprocessingobjectsarchitecturespanspan-idaudioprocessingobjectsarchitecturespanaudio-processing-objects-architecture"></a><span id="Audio_Processing_Objects_Architecture"></span><span id="audio_processing_objects_architecture"></span><span id="AUDIO_PROCESSING_OBJECTS_ARCHITECTURE"></span>音频处理对象体系结构


**音频效果的位置**

有三个不同位置的音频效果作为未实现。 它们是在 Stream 效果 (SFX)、 模式效果 (MFX) 和终结点效果 (EFX)。

**Stream 效果 (SFX)**

流效果 APO 具有实例的每个流的效果。 Stream 的效果的组合 （呈现） 之前或之后的给定模式在 tee （捕获） 而可用于更改前合成器的通道计数。 Stream 效果不用于原始流。

某些版本的 Windows，作为一种优化，不会加载 SFX 或 MFX 不在 RAW 模式。

-   Windows 8.1 不会加载原始 SFX 或原始 MFX
-   Windows 10 加载原始 MFX 但不是原始 SFX

**模式效果 (MFX)**

模式效果 (MFX) 应用于映射到相同的模式的所有流。 Tee （捕获），对于给定的模式，但在之前的组合 （呈现） 前面或后面 （呈现） 的组合或之后的所有模式下在 tee （捕获） 应用模式的效果。 应在此处放置任何方案特定的作用或不需要流效果的详细信息的效果。 它是更高的功率高效使用模式影响，因为没有为共享相同周期和格式等特征的多个流的一个实例。

**终结点生效 (EFX)**

终结点的效果 (EFX) 应用于所有使用相同的终结点的流。 终结点影响始终应用，甚至对原始流。 也就是说，它是所有模式下在 tee （捕获） 前面或后面 （呈现） 的组合。 经过认真考虑和效果应置于模式区域有疑问，应使用的终结点影响。 应在的终结点区域中放置一些影响是演讲者保护和演讲者补偿。

此图显示了流 (SFX)、 模式 (MFX) 和终结点 (EFX) 效果适用于 Windows 10 的可能位置。

![演示如何为 windows 10 中的流、 模式和终结点的效果布局的关系图](images/audio-apo-software-effects-summary.png)

**多个自定义 APO 效果**

它是可以配置多个基于 APO 效果，以使用不同的应用程序。

此图说明了如何将多个应用程序可以访问多个流、 模式和终结点 APO 效果的组合。 所有不是 COM 基于并在用户模式下运行。 在此方案中，没有任何效果在硬件或运行在内核模式下。

![显示如何将多个应用程序可以访问的流、 模式和终结点 apo 效果的多个组合的关系图](images/audio-apo-software-effects-1.png)

**请注意**  可以使用在此页的最底部滚动条以查看所有此关系图。

 

**软件模式效果和硬件终结点效果的呈现和捕获**

此图描述了软件模式效果和呈现和捕获硬件终结点效果。

![显示软件模式效果和硬件终结点效果的呈现和捕获的关系图](images/audio-apo-software-mode-effects-and-hardware-endpoint-effects-2.png)

**DSP 配备硬件产生影响的系统**

此图描述了在硬件中实施效果的 DSP 配备系统。 在此方案中，应创建代理 APO 通知硬件中实现的效果的应用。

![图示显示 dsp 配备系统硬件中实现的效果。](images/audio-apo-dsp-equipped-system-with-hardware-effects-3.png)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[Windows 音频处理对象](windows-audio-processing-objects.md)  
[实现 UI 用于配置 APO 效果](implementing-a-ui-for-configuring-apo-effects.md)  



