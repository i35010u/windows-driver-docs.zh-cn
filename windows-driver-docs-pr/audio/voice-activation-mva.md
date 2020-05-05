---
title: 多语音助手
description: 多个语音助手平台为除 Cortana 以外的其他语音助手提供支持。
ms.assetid: 48a7e96b-58e8-4a49-b673-14036d4108d5
ms.date: 03/12/2020
ms.localizationpriority: medium
ms.openlocfilehash: 828187e2569e9d366495d4805ba82948a11c2ca6
ms.sourcegitcommit: 49d7f27a24360559456063092ac35b2ba1aba7b1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82742621"
---
# <a name="multiple-voice-assistant"></a>多语音助手

多个语音助手平台为除 Cortana 以外的其他语音助手提供支持。 这允许在 Windows 设备（如电脑和可穿戴设备（如 HoloLens）上提供其他助手。 使用一组受支持的关键字模式，多个语音助手可以在同一设备上处于活动状态。

有关实现 Windows Cortana 的信息，请参阅[语音激活](voice-activation.md)。

> [!NOTE]
> 从 Windows 10 版本1903开始，支持多个语音助手。
>

## <a name="voice-activation"></a>语音激活

语音激活是一项功能，使用户能够通过口述特定短语从各种设备电源状态调用语音识别引擎。

实现语音激活是一种重要的项目，是由 SoC 供应商完成的任务。 Oem 可以联系其 SoC 供应商，了解有关其 SoC 的语音激活实现的信息。

语音激活使用户能够通过语音使用其活动上下文（即，当前屏幕上的内容）来快速参加语音助手体验。 用户经常希望能够立即访问体验，而无需与设备进行物理交互或触摸。 对于 Xbox 用户，这可能不是寻找和连接控制器。 对于 PC 用户，他们可能需要快速访问体验，而无需执行多个鼠标、触控和/或键盘操作，如厨房中的计算机。

语音激活由关键字 spotter （KWS）提供支持，它会响应是否检测到密钥短语。 关键短语可能包含关键字 "你好 Contoso"。 *关键字检测*通过硬件或软件描述关键字的检测。
关键短语本身可能失措（"你好 Contoso"）作为暂存命令，或后跟一个撰写链式命令的语音操作（"你好 Contoso，这里是我的下一会议？"）

Microsoft 提供 OS default 关键字 spotter （software 关键字 spotter），在硬件关键字检测不可用的情况下提供语音助手体验。 虽然此功能当前适用于 Cortana，但可能还需要进行其他 Microsoft 配置，以使其他语音助手加入两阶段关键字检测。 有关详细信息， `AskMVA@Microsoft.com`请联系。  

如果 KWS 是将设备从低功率状态唤醒，则此解决方案称为唤醒（WoV）。 有关详细信息，请参阅[唤醒](#wake_on_voice)。

## <a name="span-idglossary_of_termsspanspan-idglossary_of_termsspanglossary-of-terms"></a><span id="glossary_of_terms"></span><span id="Glossary_Of_Terms"></span>术语术语表

此词汇表汇总了与语音激活相关的术语。

|                      |                                                                                                                                                           |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 暂存命令 | 示例：你好，Contoso <暂停，请等待助手 UI> 天气是什么？ 这有时称为 "双拍命令" 或 "仅限关键字" |
| 链式命令 | 示例：您好，Contoso 有哪些天气？ 这有时称为 "一次" 命令 |
| 语音激活 | 示例： "你好 Contoso" 在预定义激活密钥短语中检测到关键字的方案 |
| 唤醒-语音（WoV） | 一种技术，允许从屏幕关闭语音激活，将电源状态降低到处于完全电源状态的屏幕 |
|从新式备用 WoV| 从新式备用（S0ix）屏幕关闭状态到全屏（S0）状态的唤醒 |
| 新式待机 | Windows 低功耗空闲基础结构-Windows 10 中连接备用（CS）的后续版本。 新式备用的第一种状态是在屏幕关闭时。 最深层睡眠状态是在 DRIPS/复原中。 有关详细信息，请参阅[新式备用](https://docs.microsoft.com/windows-hardware/design/device-experiences/modern-standby)|
| KWS | 关键字 spotter –提供 "你好 Contoso" 检测的算法 |
| SW KWS | Software 关键字 spotter –主机（CPU）上运行的 KWS 的实现。 对于 "你好 Cortana"，软件 KWS 包含在 Windows 中。 |
| HW KWS | 硬件关键字 spotter –在硬件上运行的 KWS 的实现 |
| 突发缓冲区 | 用于存储 PCM 数据的循环缓冲区，这些数据可在 KWS 检测的情况下 bursted，以便包括触发 KWS 检测的所有音频。 |
| 事件检测器 OEM 适配器 | 作为 Windows 语音助手堆栈和驱动程序的中介的用户模式组件 |
| 型号 | KWS 算法使用的声音模型数据文件。 数据文件为静态。 模型已本地化，每个区域设置一个。|
| MVA | 多个语音代理-新的 HWKWS DDI，支持多个代理 |
| SVA | 单个语音代理-上一个仅支持单一代理（Cortana）的 HWKWS DDI |

## <a name="span-idimplementing_voice_activationspanspan-idimplementing_voice_activationspanspan-idimplementing_voice_activationspanintegrating-a-hardware-keyword-spotter"></a><span id="Implementing_Voice_Activation"></span><span id="implementing_voice_activation"></span><span id="IMPLEMENTING_VOICE_ACTIVATION"></span>集成硬件关键字 Spotter

若要实现硬件关键字 spotter （HW KWS） SoC 供应商，必须完成以下任务。

- 根据本主题后面所述的 SYSVAD 示例创建自定义关键字检测器。 你将在 COM DLL 中实现这些方法，如[IEvent 检测器 OEM 适配器接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/eventdetectoroemadapter/nn-eventdetectoroemadapter-ieventdetectoroemadapter)中所述。
- 实现[WAVERT 增强](#wavert_enhancements)中所述的声波 RT 增强功能。
- 提供 INF 文件项来描述用于关键字检测的任何自定义项。
    - [PKEY\_FX\_KeywordDetector\_StreamEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-keyworddetector-streameffectclsid)
    - [PKEY\_FX\_KeywordDetector\_ModeEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-keyworddetector-modeeffectclsid)
    - [PKEY\_FX\_KeywordDetector\_EndpointEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-keyworddetector-endpointeffectclsid)
    - [PKEY\_SFX\_KeywordDetector\_ProcessingModes\_支持\_\_流式处理](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-sfx-keyworddetector-processingmodes-supported-for-streaming)
    - [PKEY\_MFX\_KeywordDetector\_ProcessingModes\_支持\_\_流式处理](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-mfx-keyworddetector-processingmodes-supported-for-streaming)
    - [PKEY\_EFX\_KeywordDetector\_ProcessingModes\_支持\_\_流式处理](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-efx-keyworddetector-processingmodes-supported-for-streaming)
- 在[音频设备建议](https://docs.microsoft.com/windows-hardware/design/component-guidelines/audio)中查看硬件建议和测试指南。 本主题提供用于设计和开发用于 Microsoft 语音平台的音频输入设备的指南和建议。
- 支持暂存和链式命令。
- 满足语音助手的区域设置要求
- 中（音频处理对象）必须提供以下效果： 
    -   AEC
    -   AGC
    -   NS
-   语音处理模式的效果必须由 MFX APO 报告。
-   APO 可以将格式转换作为 MFX 执行。
-   APO 必须输出以下格式：
    -   16 kHz，mono，FLOAT。
-   选择性地设计任何自定义的，以增强音频捕获过程。 有关详细信息，请参阅[Windows 音频处理对象](windows-audio-processing-objects.md)。

硬件卸载关键字 spotter （HW KWS） WoV 要求
- 在 S0 工作状态和 S0 睡眠状态也称为新式备用时，支持 HW KWS WoV。
- S3 不支持 HW KWS WoV。  

**AEC**

在捕获突发音频时，它可以由 DSP 执行，也可以在以后通过软件 APO 来完成。 若要使用 KWS 突发数据执行软件 AEC，需要在捕获突发数据时具有相应的环回音频。 为此，会为突发输出创建自定义音频格式，这会将环回音频交错为突发音频数据。

从 Windows 版本20H1 开始，Microsoft AEC APO 了解这一交错格式，并可以使用它来执行 AEC。 有关详细信息，请参阅[KSPROPERTY_INTERLEAVEDAUDIO_FORMATINFORMATION](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-interleavedaudio-formatinformation)。

**验证**

通过[语音激活管理器2测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/5119a80f-8aae-49bb-aa59-8eaa7e7b1fad)来验证[KSPROPSETID_SOUNDDETECTOR2](kspropsetid-sounddetector2.md)属性的硬件支持。

## <a name="span-idsample_code_overviewspansample-code-overview"></a><span id="sample_code_overview"></span>示例代码概述

在 GitHub 上实现语音激活的音频驱动程序的示例代码是 SYSVAD 虚拟音频适配器示例的一部分。 建议使用[此代码](https://github.com/Microsoft/Windows-driver-samples/blob/master/audio/sysvad/)作为起点。 

有关 SYSVAD 示例音频驱动程序的详细信息，请参阅[示例音频驱动程序](https://docs.microsoft.com/windows-hardware/drivers/audio/sample-audio-drivers)。

## <a name="span-idkeyword_recognition_system_informationspankeyword-recognition-system-information"></a><span id="keyword_recognition_system_information"></span>关键字识别系统信息

**语音激活音频堆栈支持**

用于启用语音激活的音频堆栈外部接口用作语音平台和音频驱动程序的通信管道。 外部接口分为三部分。

- [*事件检测程序设备驱动程序接口（DDI）*](https://docs.microsoft.com/windows-hardware/drivers/ddi/eventdetectoroemadapter/nn-eventdetectoroemadapter-ieventdetectoroemadapter)。 事件检测器设备驱动程序接口负责配置和武装 HW 关键字 Spotter （KWS）。  它还可由驱动程序用来通知系统检测事件。
- [*IEvent 检测到 OEM 适配器 DLL*](https://docs.microsoft.com/windows-hardware/drivers/ddi/eventdetectoroemadapter/nn-eventdetectoroemadapter-ieventdetectoroemadapter)。 此 DLL 实现了一个 COM 接口，用于改编驱动程序特定的不透明数据以供 OS 用于帮助进行关键字检测。
-  *WaveRT 流增强功能*。 增强功能使得音频驱动程序能够突发地流式传输来自关键字检测的缓冲音频数据。

**音频终结点属性**

音频终结点图形生成正常。 该图形准备处理的速度比实时捕获更快。 捕获的缓冲区上的时间戳始终为 true。 具体而言，时间戳会正确反映过去和缓冲时捕获的数据，现在会进行突发。

**操作理论**

驱动程序会像往常一样为其捕获设备公开 KS 筛选器。 此筛选器支持多个 KS 属性和一个 KS 事件来配置、启用和发出检测事件信号。 此筛选器还包括一个标识为关键字 spotter （KWS） pin 的附加 pin 工厂。 此 pin 用于从关键字 spotter 流式传输音频。

属性为： [ **KSPROPSETID_SoundDetector2**](kspropsetid-sounddetector2.md)

所有[**KSPROPSETID_SoundDetector2**](kspropsetid-sounddetector2.md)属性都是使用[KSSOUNDDETECTORPROPERTY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kssounddetectorproperty)数据结构调用的。 此数据结构包含 KSPROPERTY 以及要识别、重置、检测到的关键字的事件 id。

- 支持的关键字类型[**-\_KSPROPERTY\_SOUNDDETECTOR 模式**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector)。 此属性由操作系统设置，用于配置要检测的关键字。
-   关键字模式 Guid 列表- [**\_KSPROPERTY SOUNDDETECTOR\_SUPPORTEDPATTERNS**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector)。 此属性用于获取 Guid 列表，这些 Guid 用于标识支持模式的类型。
- [**KSPROPERTY\_SOUNDDETECTOR\_**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector)。 此读取/写入属性是一个简单的布尔状态，它指示是否已确定探测器。 操作系统将此设置为参与关键字检测器。 操作系统可以清除此来脱开。 如果设置了关键字模式，并且在检测到了关键字之后，驱动程序会自动清除此设置。 （操作系统必须进行重置。）
- 匹配结果- [**KSPROPERTY\_SOUNDDETECTOR\_reset**](ksproperty-sounddetector-reset.md)用于在启动时重置声音检测程序。

在关键字检测时，将发送包含 KSNOTIFICATIONID_SoundDetector 的 PNP 通知。 注意：这不是 KSEvent，而是使用负载通过 IoReportTargetDeviceChangeAsynchronous 发送的 PNP 事件。

KSNOTIFICATIONID_SoundDetector 在 ksmedia 中定义，如下所示。

```
// The payload of this notification is a SOUNDDETECTOR_DETECTIONHEADER
#define STATIC_KSNOTIFICATIONID_SoundDetector\
    0x6389d844, 0xbb32, 0x4c4c, 0xa8, 0x2, 0xf4, 0xb4, 0xb7, 0x7a, 0xfe, 0xad
DEFINE_GUIDSTRUCT("6389D844-BB32-4C4C-A802-F4B4B77AFEAD", KSNOTIFICATIONID_SoundDetector);
#define KSNOTIFICATIONID_SoundDetector DEFINE_GUIDNAMED(KSNOTIFICATIONID_SoundDetector)
```

**操作顺序**

*系统启动*

1. OS 将发送[**\_KSPROPERTY SOUNDDETECTOR\_RESET**](ksproperty-sounddetector-reset.md)以清除任何以前的检测状态，将所有检测程序重置为已卸下并清除以前的模式集。
2. OS 查询[**\_KSPROPERTY SOUNDDETECTOR\_模式**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector)以检索事件检测器 OEM 适配器的 clsid。
3. 操作系统使用事件检测到 oem 适配器来检索支持的关键字和语言的列表。
4. 操作系统注册驱动程序发送的自定义 PNP 通知
5. OS 设置必需的关键字模式。
6. 操作系统会对检测

**内部驱动程序和硬件操作**

尽管检测到了探测器，但硬件可以在小型 FIFO 缓冲区中持续捕获和缓冲音频数据。 （此 FIFO 缓冲区的大小由本文档之外的要求确定，但通常为数百毫秒到几秒钟。）检测算法通过此缓冲区对数据流进行操作。 驱动程序和硬件的设计是这样的，尽管在检测到关键字之前，驱动程序与硬件之间没有任何交互，也不会中断到 "应用程序" 处理器。 这允许系统在没有其他活动的情况下接通电源状态。

当硬件检测到某个关键字时，它会生成一个中断。 在等待驱动程序为中断提供服务的同时，硬件将继续将音频捕获到缓冲区中，并确保关键字在超过缓冲限制的情况下不会丢失任何数据。

**关键字时间戳**

在检测关键字之后，所有语音激活解决方案都必须在关键字开头之前缓冲所有口述关键字，包括1.6。 音频驱动程序必须提供标识流中关键短语的开始和结束时间的时间戳。

为了支持关键字的开始/结束时间戳，DSP 软件可能需要基于 DSP 时钟的内部时间戳事件。 一旦检测到了某个关键字，DSP 软件就会与该驱动程序交互以准备 KS 事件。 驱动程序和 DSP 软件需要将 DSP 时间戳映射到 Windows 性能计数器值。 执行此操作的方法特定于硬件设计。 一种可能的解决方案是，驱动程序读取当前性能计数器、查询当前 DSP 时间戳、再次读取当前性能计数器，然后估计性能计数器和 DSP 时间之间的相关性。 然后，根据相关关系，驱动程序可以将关键字 DSP 时间戳映射到 Windows 性能计数器时间戳。


## <a name="span-idievent_detectorspanievent-detector-oem-adapter-interface"></a><span id="ievent_detector"></span>IEvent 检测器 OEM 适配器接口

OEM 提供一个 COM 对象实现，它充当 OS 和驱动程序之间的中介，有助于计算或分析通过[**\_KSPROPERTY SOUNDDETECTOR\_模式**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-patterns)和[**KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-matchresult)写入和读取到音频驱动程序的不透明数据。

COM 对象的 CLSID 是由[**\_KSPROPERTY SOUNDDETECTOR\_SUPPORTEDPATTERNS**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-supportedpatterns)返回的探测器模式类型 GUID。 OS 调用 CoCreateInstance，传递模式类型 GUID 来实例化与关键字模式类型兼容的适当 COM 对象，并调用对象的 IEventDetectorOemAdapter 接口上的方法。

**COM 线程模型要求**

OEM 的实现可以选择任何 COM 线程模型。

**IEventDetectorOemAdapter**

接口设计会尝试使对象实现保持无状态。 换句话说，实现应要求在方法调用之间不存储任何状态。 事实上，内部 c + + 类可能不需要除实现 COM 对象所需的所有成员变量。

**方法**

实现以下方法。

-   [**IEventDetectorOemAdapter::BuildArmingPatternData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/eventdetectoroemadapter/nf-eventdetectoroemadapter-ieventdetectoroemadapter-buildarmingpatterndata)
-   [**IEventDetectorOemAdapter::ComputeAndAddUserModelData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/eventdetectoroemadapter/nf-eventdetectoroemadapter-ieventdetectoroemadapter-computeandaddusermodeldata)
-   [**IEventDetectorOemAdapter：： GetCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/eventdetectoroemadapter/nf-eventdetectoroemadapter-ieventdetectoroemadapter-getcapabilities)
-   [**IEventDetectorOemAdapter::GetCapabilitiesForLanguage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/eventdetectoroemadapter/nf-eventdetectoroemadapter-ieventdetectoroemadapter-getcapabilitiesforlanguage)
-   [**IEventDetectorOemAdapter：:P arseDetectionResultData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/eventdetectoroemadapter/nf-eventdetectoroemadapter-ieventdetectoroemadapter-parsedetectionresultdata)
-   [**IEventDetectorOemAdapter::ReportOSDetectionResult**](https://docs.microsoft.com/windows-hardware/drivers/ddi/eventdetectoroemadapter/nf-eventdetectoroemadapter-ieventdetectoroemadapter-parsedetectionresultdata)
-   [**IEventDetectorOemAdapter::VerifyUserEventData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/eventdetectoroemadapter/nf-eventdetectoroemadapter-ieventdetectoroemadapter-verifyusereventdata)

## <a name="span-idwavert_enhancementsspanspan-idwavert_enhancementsspanspan-idwavert_enhancementsspanwavert-enhancements"></a><span id="WAVERT_Enhancements"></span><span id="wavert_enhancements"></span><span id="WAVERT_ENHANCEMENTS"></span>WAVERT 增强功能

小型端口接口定义为由 WaveRT 微型端口驱动程序实现。 这些接口提供了简化音频驱动程序的方法，改进了 OS 音频管道的性能和可靠性，或支持新的方案。 定义了一个新的 PnP 设备接口属性，该属性允许驱动程序向操作系统提供其缓冲区大小约束的静态表达式。

**缓冲区大小**

在操作系统、驱动程序和硬件之间移动音频数据时，驱动程序在各种约束下运行。 这些限制可能是由于物理硬件传输在内存和硬件间移动数据，以及/或者由于硬件或关联的 DSP 中的信号处理模块导致的。

硬件-KWS 解决方案至少必须支持100ms 和200毫秒的音频捕获大小。

驱动程序通过在包含 KS 流式处理 pin 的 KS\_筛选\_器\_的 KSCATEGORY\_音频 PnP 设备接口上设置 DEVPKEY KsAudio PacketSize 约束设备属性来表示缓冲区大小约束。 当启用了 KS 筛选器接口时，此属性应保持有效且稳定。 操作系统可以随时读取此值，而无需打开驱动程序的句柄并对驱动程序调用。

**DEVPKEY\_KsAudio\_PacketSize\_约束**

DEVPKEY\_KsAudio\_PacketSize\_约束属性值包含一个[**KsAudio\_PacketSize\_约束**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints)结构，该结构描述物理硬件约束（例如，由于将数据从 WaveRT 缓冲区传输到音频硬件的机制）。 此结构包含一个数组，其中包含0个或多个[**KSAUDIO\_\_PACKETSIZE PROCESSINGMODE\_约束**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_signalprocessingmode_constraint)结构，其中描述了特定于任何信号处理模式的约束。 驱动程序在调用[**PcRegisterSubdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregistersubdevice)之前设置此属性，或以其他方式为其流式处理 pin 启用其 KS 筛选器接口。

**IMiniportWaveRTInputStream**

驱动程序实现此接口，以便更好地协调从驱动程序到操作系统的音频数据流。 如果此接口在捕获流中可用，则操作系统将使用此接口上的方法访问 WaveRT 缓冲区中的数据。 有关详细信息，请参阅[ **IMiniportWaveRTInputStream：： GetReadPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket)

**IMiniportWaveRTOutputStream**

WaveRT 微型端口可以选择实现此接口，以便建议从 OS 写入进度并返回准确的流位置。 有关详细信息，请参阅[**IMiniportWaveRTOutputStream：： SetWritePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertoutputstream-setwritepacket)、 [**IMiniportWaveRTOutputStream：： GetOutputStreamPresentationPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertoutputstream-getoutputstreampresentationposition)和[**IMiniportWaveRTOutputStream：： GetPacketCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertoutputstream-getpacketcount)。

**性能计数器时间戳**

几个驱动程序例程返回 Windows 性能计数器时间戳，反映设备捕获或显示样本的时间。

在具有复杂的 DSP 管道和信号处理的设备中，计算准确的时间戳可能会很困难，应周全完成。 时间戳不应简单地反映从 OS 向 DSP 传输样本的时间。

- 在 DSP 内，使用某种内部的 DSP 墙壁跟踪示例时间戳。
- 在驱动程序和 DSP 之间，计算 Windows 性能计数器和 DSP 墙壁时钟之间的关联。 此过程的过程包括非常简单（但不精确）到相当复杂或 novel （但更精确）。
- 由于信号处理算法、管道或硬件传输而导致的任何常量延迟，除非其他情况下会考虑这些延迟。

**突发读取操作**

本部分介绍了突发读取的操作系统和驱动程序交互。 只要驱动程序支持基于数据包的流式处理 WaveRT 模型（包括[**IMiniportWaveRTInputStream：： GetReadPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket)函数），就可以在语音激活方案之外执行突发读取。

讨论了两次突发示例读取方案。 在一种方案中，如果微型端口支持 pin 类别为[**KSNODETYPE\_AUDIO\_KEYWORDDETECTOR**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-audio-keyworddetector)的 pin，则在检测到关键字时，驱动程序将开始捕获和内部缓冲数据。 在另一种情况下，如果 OS 不是通过调用[**IMiniportWaveRTInputStream：： GetReadPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket)更快地读取数据，则驱动程序可以有选择地在 WaveRT 缓冲区之外缓冲数据。

若要突发在转换到 KSSTATE\_运行之前捕获的数据，驱动程序必须保留准确的示例时间戳信息以及缓冲捕获数据。 时间戳标识捕获样本的即时采样。

1. 流过渡到 KSSTATE\_运行后，该驱动程序会立即设置缓冲区通知事件，因为它已经有可用数据。
2. 在此事件中，操作系统将调用 GetReadPacket （）来获取有关可用数据的信息。

    a. 驱动程序将返回有效捕获的数据（0表示从 KSSTATE\_STOP 转换到 KSSTATE\_运行后的第一个数据包）的数据包号，操作系统可从该数据派生 WaveRT 缓冲区内的数据包位置以及相对于流开始的数据包位置。

    b. 驱动程序还会返回性能计数器值，该值对应于数据包中第一个样本的采样瞬时。 请注意，此性能计数器值可能相对较旧，这取决于在硬件或驱动程序（WaveRT 缓冲区之外）缓冲捕获数据的程度。

    c. 如果有更多未读缓冲数据可用，则为： i。 立即将此数据传输到 WaveRT 缓冲区的可用空间（即，未由 GetReadPacket 返回的数据包使用的空间），对 MoreData 返回 true，并在从该例程返回之前设置缓冲区通知事件。 或 ii。 计划硬件将下一个数据包传输到 WaveRT 缓冲区的可用空间中，为 MoreData 返回 false，并在传输完成时设置 buffer 事件。
3. 操作系统使用 GetReadPacket （）返回的信息从 WaveRT 缓冲区读取数据。
4. OS 等待下一个缓冲区通知事件。 如果驱动程序在步骤中设置了缓冲区通知，等待可能会立即终止。
5. 如果驱动程序没有在步骤（2c）中立即设置事件，则驱动程序会在将更多捕获的数据传输到 WaveRT 缓冲区并使其可供 OS 读取时设置事件。
6. 请参阅（2）。

对于[**KSNODETYPE\_audio\_KEYWORDDETECTOR**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-audio-keyworddetector)关键字检测器引脚，驱动程序应为至少 5000 ms 的音频数据分配足够的内部突发缓冲。 如果在缓冲区溢出之前，操作系统无法在 pin 上创建流，则驱动程序可能会结束内部缓冲活动和可用的关联资源。

## <a name="span-idwake_on_voicespanspan-idwake_on_voicespanspan-idwake_on_voicespanwake-on-voice"></a><span id="Wake_on_Voice"></span><span id="wake_on_voice"></span><span id="WAKE_ON_VOICE"></span>唤醒

通过使用唤醒（WoV），用户可以通过说出特定关键字（如 "你好 Contoso"），从低功耗状态中激活语音识别引擎，并在屏幕上进行查询。

此功能允许设备在设备处于空闲状态且屏幕关闭时始终倾听用户的声音。 这是由于侦听模式与正常的麦克风录制相比，使用的功率更少。 WoV 允许链接语音短语，如 "你好 Contoso，当我下一次约会时"，它将以无人参与的方式调用语音助手的响应。

音频堆栈负责传达唤醒数据（发言人 ID、关键字触发器和置信度的上下文信息），并通知感兴趣的客户端已检测到关键字。

**新式备用系统上的验证**

可在[新式备用](https://docs.microsoft.com/windows-hardware/design/device-experiences/modern-standby)系统上使用[针对 AC 电源的新式备用唤醒基本测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/69df7cf2-6024-4eee-92ee-1506480614ee)来验证来自系统空闲状态的 WoV，并在[HLK](https://docs.microsoft.com/windows-hardware/test/hlk/)中的[DC 电源上检测新式备用唤醒](https://docs.microsoft.com/windows-hardware/test/hlk/testref/614ffb93-eced-45ab-bf7b-e09291a97fd2)基本测试。 这些测试检查系统是否具有硬件关键字 spotter （HW-KWS），是否能够进入最深的运行时空闲平台状态（DRIPS），并且能够从具有小于或等于1秒的系统恢复延迟的新式备用声音命令中唤醒。
