---
title: 音频处理对象体系结构
description: 音频处理对象的体系结构用于 Windows 音频流的基于软件的数字信号处理。
ms.assetid: 2F57B4C7-8C83-4DDF-BFAF-B9308752E91D
ms.date: 10/18/2019
ms.localizationpriority: medium
ms.openlocfilehash: 194456691708c58be427e8c2d3f1757e2a2341d1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208305"
---
# <a name="audio-processing-object-architecture"></a>音频处理对象体系结构

音频处理对象 () ，为 Windows 音频流提供可自定义的基于软件的数字信号处理。

## <a name="span-idaudio_processing_objects_overviewspanspan-idaudio_processing_objects_overviewspanspan-idaudio_processing_objects_overviewspanaudio-processing-objects-overview"></a><span id="Audio_Processing_Objects_Overview"></span><span id="audio_processing_objects_overview"></span><span id="AUDIO_PROCESSING_OBJECTS_OVERVIEW"></span>音频处理对象概述

Windows 允许 Oem 和第三方音频硬件制造商将自定义数字信号处理效果作为其音频驱动程序增值功能的一部分包含在内。 这些效果打包为用户模式系统效果音频处理对象 (的) 。

音频处理对象 (是) ，为 Windows 音频流提供基于软件的数字信号处理。 APO 是一个 COM 主机对象，该对象包含一个算法，该算法旨在提供特定数字信号处理 (DSP) 效果。 此功能非正式地称为 "音频效果"。 的示例包括图形 equalizers、回音、tremolo、回声)  (AEC 和自动增益控制 (AGC) 。 是基于 COM 的实时进程内对象。

**注意**   本文档中的说明和术语主要涉及输出设备。 不过，这种技术是对称的，并在本质上适用于输入设备。

**软件与硬件 DSP**

) 的硬件数字信号处理器 (DSP 是专用的微处理器 (或 SIP 块) ，其体系结构针对数字信号处理的操作需要进行了优化。 在专门构建的硬件与使用软件 APO，实现音频处理可能会有很大的优势。 一个优点是，使用硬件实现的 DSP 可能降低 CPU 使用情况和关联功率消耗。

在实现基于软件的 APO 之前，需要考虑其他一些优点和缺点，这些都是你的项目目标和约束。

基于软件的效果在流初始化时插入软件设备管道中。 这些解决方案会对主 CPU 处理其所有效果，而不依赖于外部硬件。 当驱动程序和硬件仅支持原始处理时，这种类型的解决方案最适用于传统的 Windows 音频解决方案，如 HDAudio、USB 和蓝牙设备。 有关原始处理的详细信息，请参阅 [音频信号处理模式](audio-signal-processing-modes.md)。

**用于硬件 DSP 的代理 APO**

在硬件 DSP 中应用的任何效果都需要通过代理 APO 播发。 Microsoft 提供了默认的代理 APO ( # A0) 。 若要使用 Microsoft 提供的 APO，必须支持此属性集和属性。

-   [KSPROPSETID \_ AudioEffectsDiscovery](./kspropsetid-audioeffectsdiscovery.md)
-   [KSPROPERTY \_ AUDIOEFFECTSDISCOVERY \_ EFFECTSLIST](/previous-versions/windows/hardware/drivers/dn457706(v=vs.85))

或者，您可以实现自己的代理 APO。

**Windows 提供 (系统) **

Windows 安装了一组默认的 "中"，提供了许多不同的音频效果。 有关系统提供的 APO 效果的列表，请参阅 [音频信号处理模式](audio-signal-processing-modes.md)。

Oem 可以包含所有提供的系统，或将其部分或全部替换为自定义的。

**自定义**

通过添加其他音频效果，可以创建自定义的 "中" 来增强 Windows 音频体验。

OEM 可以在交付 Windows 时包含提供的 Windows 的任意组合。

自定义 APO 可以由 OEM 或第三方安装，以便在购买设备后提高音频体验。 当用户使用标准 INF 文件安装音频设备驱动程序时，它们将自动具有对系统的访问权限。 独立硬件供应商 (Ihv) 和原始设备制造商 (Oem) 可以在仍使用 Microsoft 类驱动程序的同时提供额外的自定义系统影响。 它们通过将其 DSP 算法打包为并修改标准 INF 文件来实现此目的，以将其插入到音频引擎的信号处理图形中。

有关创建自定义的详细信息，请参阅 [实现音频处理对象](implementing-audio-processing-objects.md)。

**自定义 APO 支持应用**

若要允许用户配置与自定义 APO 关联的设置，建议的方法是创建硬件支持应用。 有关详细信息，请参阅 [硬件支持应用 (HSA) ：驱动程序开发人员的步骤](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)。

**自定义 APO 测试和要求**

Microsoft HLK 提供可用于的测试。 有关音频测试的详细信息，请参阅 [设备。音频](/previous-versions/windows/hardware/hck/jj123955(v=vs.85)) 测试和 [设备。音频](/previous-versions/windows/hardware/hck/jj124726(v=vs.85))测试。

使用时，这两种测试可能特别有用。

[验证音频 EffectsDiscovery (手动) 认证](/previous-versions/windows/hardware/hck/dn456312(v=vs.85))

[SysFX 测试](/previous-versions/windows/hardware/hck/jj124017(v=vs.85))

有关支持的音频要求的信息，请参阅 [设备。音频要求](/previous-versions/windows/hardware/cert-program/deviceaudio-requirements)。

**自定义 APO 工具和实用程序**

您可以使用 "音频效果发现示例" 来浏览可用的音频效果。 此示例演示如何在呈现和捕获音频设备上查询音频效果，以及如何监视音频效果的变化。 它作为 SDK 示例的一部分提供，可以使用以下链接下载：

[音频效果发现示例](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/411c271e537727d737a53fa2cbe99eaecac00cc0/Official%20Windows%20Platform%20Sample/Audio%20effects%20discovery%20sample)

**应用程序音频效果感知**

应用程序可以调用 Api 来确定哪些音频效果当前在系统上处于活动状态。 有关音频效果感知 Api 的详细信息，请参阅 [AudioRenderEffectsManager 类](/uwp/api/Windows.Media.Effects.AudioRenderEffectsManager)。

## <a name="span-idaudio_processing_objects_architecturespanspan-idaudio_processing_objects_architecturespanspan-idaudio_processing_objects_architecturespanaudio-processing-objects-architecture"></a><span id="Audio_Processing_Objects_Architecture"></span><span id="audio_processing_objects_architecture"></span><span id="AUDIO_PROCESSING_OBJECTS_ARCHITECTURE"></span>音频处理对象体系结构

**音频效果的位置**

有三个用于实现的音频效果的不同位置。 它们处于流效果， (SFX) 、模式效果 (MFX) 和端点效果 (EFX) 。

** (SFX) 的流效果 **

流效果 APO 的每个流都有一个效果的实例。 流效果在混合 (呈现) 之前或之后 (捕获给定模式的) ，并可用于在混音器之前更改通道计数。 流效果不用于原始流。

某些版本的 Windows 作为一种优化方式，不会在 RAW 模式下加载 MFX 或。

-   Windows 8.1 不加载原始 SFX 或原始 MFX
-   Windows 10 加载原始 MFX，但不加载原始 SFX

**模式效果 (MFX) **

将 MFX)  (的模式效果应用于映射到相同模式的所有流。 模式效果在混合 (呈现) 之前或之前应用， (在给定模式下捕获) 之前，但在 (之前或之后) 捕获所有模式的 (之前。 不需要流效果具体的任何具体方案或效果都应放置在此处。 使用模式效果更为强大，因为有多个流的一个实例共享相同的特性（如周期和格式）。

**EFX)  (的端点效果 **

将 EFX)  (的端点效果应用到使用同一终结点的所有流。 始终应用终结点效果，甚至应用于原始流。 也就是说，在混合 (呈现) 或之前， (在所有模式下捕获) 。 应谨慎使用终结点效果，并在不确定应将效果放入模式区域。 应放置在终结点区域中的一些效果是扬声器保护和扬声器补偿。

此图显示了适用于 Windows 10 的 stream (SFX) 、mode (MFX) 和 endpoint (EFX) 效果的可能位置。

![演示如何在 windows 10 中提供流、模式和端点效果的布局的示意图](images/audio-apo-software-effects-summary.png)

**多个自定义 APO 效果**

可以配置多个基于 APO 的效果，以处理不同的应用程序。

此图说明了多个应用程序如何可以访问多个 stream、mode 和 endpoint APO 效果组合。 所有的都是基于 COM 的，并在用户模式下运行。 在此方案中，没有任何效果在硬件或内核模式下运行。

![显示多个应用程序如何可以访问 stream、mode 和 endpoint apo 效果的多个组合的关系图](images/audio-apo-software-effects-1.png)

**注意**   您可以使用此页底部的滚动条来查看此关系图。

**用于呈现和捕获的软件模式效果和硬件终结点效果**

此图说明了用于呈现和捕获的软件模式效果和硬件终结点效果。

![显示用于呈现和捕获的软件模式效果和硬件终结点效果的关系图](images/audio-apo-software-mode-effects-and-hardware-endpoint-effects-2.png)

**配备有硬件影响的 DSP 系统**

此图说明了在硬件中实现影响的 DSP 系统。 在这种情况下，应创建代理 APO 以通知应用在硬件中实现的效果。

![此图显示了在硬件中实现影响的 dsp 配备的系统。](images/audio-apo-dsp-equipped-system-with-hardware-effects-3.png)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[Windows 音频处理对象](windows-audio-processing-objects.md)