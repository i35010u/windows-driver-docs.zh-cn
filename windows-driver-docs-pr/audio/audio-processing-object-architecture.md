---
title: 音频处理对象体系结构
description: 音频处理对象（即）为 Windows 音频流提供可自定义的基于软件的数字信号处理。
ms.assetid: 2F57B4C7-8C83-4DDF-BFAF-B9308752E91D
ms.date: 10/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5f89a0c8a87f4f071610eec6021c0016decdd4c0
ms.sourcegitcommit: 9ebed9a7909b0e39a0efb1c23a5435bf36688d05
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/06/2019
ms.locfileid: "74898494"
---
# <a name="audio-processing-object-architecture"></a>音频处理对象体系结构

音频处理对象（即）为 Windows 音频流提供可自定义的基于软件的数字信号处理。

## <a name="span-idaudio_processing_objects_overviewspanspan-idaudio_processing_objects_overviewspanspan-idaudio_processing_objects_overviewspanaudio-processing-objects-overview"></a><span id="Audio_Processing_Objects_Overview"></span><span id="audio_processing_objects_overview"></span><span id="AUDIO_PROCESSING_OBJECTS_OVERVIEW"></span>音频处理对象概述

Windows 允许 Oem 和第三方音频硬件制造商将自定义数字信号处理效果作为其音频驱动程序增值功能的一部分包含在内。 这些效果打包为用户模式系统效果音频处理对象（即）。

音频处理对象（即）为 Windows 音频流提供基于软件的数字信号处理。 APO 是一个 COM 主机对象，该对象包含一个算法，该算法是为了提供特定数字信号处理（DSP）效果而编写的。 此功能非正式地称为 "音频效果"。 的示例包括图形 equalizers、回音、tremolo、回声取消（AEC）和自动增益控制（AGC）。 是基于 COM 的实时进程内对象。

**请注意**，本文档中的说明和术语主要指的是输出设备的  。 不过，这种技术是对称的，并在本质上适用于输入设备。

**软件与硬件 DSP**

硬件数字信号处理器（DSP）是一个专用微处理器（或 SIP 块），其体系结构针对数字信号处理的操作需要进行了优化。 在专门构建的硬件与使用软件 APO，实现音频处理可能会有很大的优势。 一个优点是，使用硬件实现的 DSP 可能降低 CPU 使用情况和关联功率消耗。

在实现基于软件的 APO 之前，需要考虑其他一些优点和缺点，这些都是你的项目目标和约束。

基于软件的效果在流初始化时插入软件设备管道中。 这些解决方案会对主 CPU 处理其所有效果，而不依赖于外部硬件。 当驱动程序和硬件仅支持原始处理时，这种类型的解决方案最适用于传统的 Windows 音频解决方案，如 HDAudio、USB 和蓝牙设备。 有关原始处理的详细信息，请参阅[音频信号处理模式](audio-signal-processing-modes.md)。

**用于硬件 DSP 的代理 APO**

在硬件 DSP 中应用的任何效果都需要通过代理 APO 播发。 Microsoft 提供了一个默认代理 APO （MsApoFxProxy）。 若要使用 Microsoft 提供的 APO，必须支持此属性集和属性。

-   [KSPROPSETID\_AudioEffectsDiscovery](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-audioeffectsdiscovery)
-   [KSPROPERTY\_AUDIOEFFECTSDISCOVERY\_EFFECTSLIST](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn457706(v=vs.85))

或者，您可以实现自己的代理 APO。

**Windows 提供的（系统）**

Windows 安装了一组默认的 "中"，提供了许多不同的音频效果。 有关系统提供的 APO 效果的列表，请参阅[音频信号处理模式](audio-signal-processing-modes.md)。

Oem 可以包含所有提供的系统，或将其部分或全部替换为自定义的。

**自定义**

通过添加其他音频效果，可以创建自定义的 "中" 来增强 Windows 音频体验。

OEM 可以在交付 Windows 时包含提供的 Windows 的任意组合。

自定义 APO 可以由 OEM 或第三方安装，以便在购买设备后提高音频体验。 当用户使用标准 INF 文件安装音频设备驱动程序时，它们将自动具有对系统的访问权限。 独立硬件供应商（Ihv）和原始设备制造商（Oem）可以在仍使用 Microsoft 类驱动程序的同时提供其他自定义系统效果。 它们通过将其 DSP 算法打包为并修改标准 INF 文件来实现此目的，以将其插入到音频引擎的信号处理图形中。

有关创建自定义的详细信息，请参阅[实现音频处理对象](implementing-audio-processing-objects.md)。

**自定义 APO 支持应用**

若要允许用户配置与自定义 APO 关联的设置，建议的方法是创建硬件支持应用。 有关详细信息，请参阅[硬件支持应用（HSA）：驱动程序开发人员的步骤](https://docs.microsoft.com/windows-hardware/drivers/devapps/hardware-support-app--hsa--steps-for-driver-developers)。

**自定义 APO 测试和要求**

Microsoft HLK 提供可用于的测试。 有关音频测试的详细信息，请参阅[设备。音频](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj123955(v=vs.85))测试和[设备。音频](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124726(v=vs.85))测试。

使用时，这两种测试可能特别有用。

[验证音频 EffectsDiscovery （手动）-认证](https://docs.microsoft.com/previous-versions/windows/hardware/hck/dn456312(v=vs.85))

[SysFX 测试](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124017(v=vs.85))

有关支持的音频要求的信息，请参阅[设备。音频要求](https://docs.microsoft.com/previous-versions/windows/hardware/cert-program/deviceaudio-requirements)。

**自定义 APO 工具和实用程序**

您可以使用 "音频效果发现示例" 来浏览可用的音频效果。 此示例演示如何在呈现和捕获音频设备上查询音频效果，以及如何监视音频效果的变化。 它作为 SDK 示例的一部分提供，可以使用以下链接下载：

[音频效果发现示例](https://go.microsoft.com/fwlink/p/?linkid=2112597)

**应用程序音频效果感知**

应用程序可以调用 Api 来确定哪些音频效果当前在系统上处于活动状态。 有关音频效果感知 Api 的详细信息，请参阅[AudioRenderEffectsManager 类](https://docs.microsoft.com/uwp/api/Windows.Media.Effects.AudioRenderEffectsManager)。

## <a name="span-idaudio_processing_objects_architecturespanspan-idaudio_processing_objects_architecturespanspan-idaudio_processing_objects_architecturespanaudio-processing-objects-architecture"></a><span id="Audio_Processing_Objects_Architecture"></span><span id="audio_processing_objects_architecture"></span><span id="AUDIO_PROCESSING_OBJECTS_ARCHITECTURE"></span>音频处理对象体系结构

**音频效果的位置**

有三个用于实现的音频效果的不同位置。 它们处于流效果（SFX）、模式效果（MFX）和终结点效果（EFX）中。

**流效果（SFX）**

流效果 APO 的每个流都有一个效果的实例。 流效果位于给定模式下的组合（呈现）或后（捕获）之前，可用于更改混音器前面的通道计数。 流效果不用于原始流。

某些版本的 Windows 作为一种优化方式，不会在 RAW 模式下加载 MFX 或。

-   Windows 8.1 不加载原始 SFX 或原始 MFX
-   Windows 10 加载原始 MFX，但不加载原始 SFX

**模式效果（MFX）**

模式效果（MFX）将应用于映射到相同模式的所有流。 模式效果应用于给定模式下的组合（呈现）或在 t 形（捕获）之前，但在组合（render）之前或在所有模式的 "t" （捕获）之后。 不需要流效果具体的任何具体方案或效果都应放置在此处。 使用模式效果更为强大，因为有多个流的一个实例共享相同的特性（如周期和格式）。

**终结点效果（EFX）**

终结点效果（EFX）应用于使用同一终结点的所有流。 始终应用终结点效果，甚至应用于原始流。 也就是说，它是在所有模式的组合（呈现）之后或在所有模式的 "t" （捕获）之前。 应谨慎使用终结点效果，并在不确定应将效果放入模式区域。 应放置在终结点区域中的一些效果是扬声器保护和扬声器补偿。

此图显示了适用于 Windows 10 的流（SFX）、模式（MFX）和终结点（EFX）效果的可能位置。

![演示如何在 windows 10 中提供流、模式和端点效果的布局的示意图](images/audio-apo-software-effects-summary.png)

**多个自定义 APO 效果**

可以配置多个基于 APO 的效果，以处理不同的应用程序。

此图说明了多个应用程序如何可以访问多个 stream、mode 和 endpoint APO 效果组合。 所有的都是基于 COM 的，并在用户模式下运行。 在此方案中，没有任何效果在硬件或内核模式下运行。

![显示多个应用程序如何可以访问 stream、mode 和 endpoint apo 效果的多个组合的关系图](images/audio-apo-software-effects-1.png)

**请注意**  可以使用此页面最底部的滚动条来查看此关系图。

**用于呈现和捕获的软件模式效果和硬件终结点效果**

此图说明了用于呈现和捕获的软件模式效果和硬件终结点效果。

![显示用于呈现和捕获的软件模式效果和硬件终结点效果的关系图](images/audio-apo-software-mode-effects-and-hardware-endpoint-effects-2.png)

**配备有硬件影响的 DSP 系统**

此图说明了在硬件中实现影响的 DSP 系统。 在这种情况下，应创建代理 APO 以通知应用在硬件中实现的效果。

![此图显示了在硬件中实现影响的 dsp 配备的系统。](images/audio-apo-dsp-equipped-system-with-hardware-effects-3.png)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[Windows 音频处理对象](windows-audio-processing-objects.md)  
