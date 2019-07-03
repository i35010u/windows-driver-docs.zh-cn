---
title: 语音激活
description: Cortana，Cortana 和听写等 Windows 10 中的语音平台用于支持语音的所有 Windows 体验。
ms.assetid: 0684EF32-AA76-418B-9027-1C067A8140E3
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 22a1d0ac36df21b55fddd10b42f662533ee94eb9
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518735"
---
# <a name="voice-activation"></a>语音激活

2013 中的第一次在 Microsoft BUILD 开发人员会议演示 Cortana，个人助理技术。 Windows 语音平台使用幂等 Cortana 和听写的 Windows 10 中的所有语音体验。 语音激活是一项功能，使用户能够通过说特定内容中的调用语音识别引擎从各种设备的电源状态"你好，小娜"。 若要创建支持语音激活技术的硬件，请查看本主题中的信息。

**注意**  
实现语音激活是一项重大项目，在任务完成 SoC 供应商。 Oem 可以联系其 SoC 供应商有关其 SoC 实现语音激活的信息。


## <a name="span-idcortanaenduserexperiencecortana-end-user-experience"></a><span id="cortana_end_user_experience">Cortana 最终用户体验


若要了解在 Windows 中可用的语音交互体验，查阅这些主题。

|                                                                                                   |                                                                       |
|---------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------|
| **Topic**                                                                                         | **说明**                                                       |
| [什么是 Cortana？](https://support.microsoft.com/help/17214/cortana-what-is)      | 提供并为 Cortana 而设的概述和使用情况的方向                 |
| [您使 Cortana](https://support.microsoft.com/help/17178/windows-10-make-cortana-yours) | 介绍自定义可通过 Cortana 的设置屏幕。 |



## <a name="span-idintroductiontoheycortanavoiceactivationandlearnmyvoicespanintroduction-to-hey-cortana-voice-activation-and-learn-my-voice"></a><span id="introduction_to__hey_cortana__voice_activation_and__learn_my_voice_"></span>"你好，小娜"语音激活和"了解我的语音"简介


**"您好 Cortana"语音激活**

"你好，小娜"语音激活 (VA) 功能允许用户快速吸引其活动的上下文 （即，什么是当前在屏幕上） 之外的 Cortana 体验使用他或她的声音。 用户通常想要能够立即访问体验而无需以物理方式进行交互触摸设备。 这可能是由于在汽车中驱动并让手机用户其关注和人工参与与操作系统车辆。 Xbox 用户，这可能是由于不想要查找并连接一个控制器。 对于 PC 用户，这可能是由于对一种体验的快速访问而无需执行多个鼠标、 触控和/或键盘操作，例如在厨房中使用的计算机。

语音激活提供通过预定义的关键短语或"激活短语"始终侦听语音输入。 关键短语可能失措本身 （"你好，小娜"） 为分阶段的命令，或跟语音操作，例如，"你好，小娜，其中，是我下一次会议？"、 一个命令链接在一起。

术语*关键字检测*，由硬件或软件描述关键字的检测。

*关键字仅*激活发生时仅 Cortana 关键字所说，Cortana 启动和 EarCon 声音，以指示它已进入侦听模式。

一个*链接命令*描述颁发紧跟关键字的命令的能力 (如"你好，小娜调用 John") 和具有 Cortana 启动 （如果尚未启动），按照 （从电话呼叫开始 John） 的命令。

此图描述了链接和关键字仅激活。

![链接和关键字激活显示音频缓冲区关系图和时间序列](images/audio-chained-keyword-activation.png)

Microsoft 提供了以确保质量的硬件关键字检测并提供在其中硬件关键字检测为不存在或不可用的情况下你好，小娜体验使用操作系统默认关键字 spotter (软件关键字 spotter)。 

**"了解我的语音"功能**

"了解我的语音"功能允许用户以训练 Cortana 以识别其唯一的声音。 这通过用户单击来实现*了解如何我说"你好，小娜"* Cortana 设置屏幕中。 然后，用户重复提供了足够的各种拼音模式用于标识用户语音的唯一特性的六个谨慎选择的短语。

![hw 关键字 spotter cortana 桌面设置唤醒语音](images/audio-voice-activation-settings-2017.png)

当语音激活配对使用"了解我的语音"，这两种算法将协同工作，以减少 false 激活。 这是重要作用会议空间方案中，其中一个人说"你好，小娜"在完整的房间内的设备。

语音激活由做出响应，如果检测到的关键短语关键字 spotter (KWS) 提供支持。 如果 KWS 将唤醒从低功率状态的设备，该解决方案被称为唤醒语音 (WoV)。 有关详细信息，请参阅[唤醒语音](#wake_on_voice)。


## <a name="span-idglossaryoftermsspanspan-idglossaryoftermsspanglossary-of-terms"></a><span id="glossary_of_terms"></span><span id="Glossary_Of_Terms"></span>术语词汇表

此术语表总结了与语音激活相关的术语。

|                      |                                                                                                                                                           |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 分阶段的命令        | 例如：您好 Cortana < 暂停，等待 earcon > 天气是什么？ 这有时称为"两个截图命令"或"仅关键字" |
|链接的命令        | 例如：您好 Cortana 天气是什么？ 这有时称为"单步命令" |
| 语音激活      | 提供的预定义的激活关键短语的关键字检测的方案。 例如，"你好，小娜"是 Microsoft 语音激活方案。 |
|WoV                    | 唤醒-上的语音 – 到屏幕上完整的电源状态从屏幕关闭节能状态，启用语音激活的技术。 |
|WoV 从现代待机状态| 唤醒-上的语音从关闭状态的现代待机状态 (S0ix) 屏幕到屏幕的全部功能 (S0) 状态。 |
|新式待机 |Windows 低电源空闲基础结构的后继到连接待机状态 (CS) 在 Windows 10。 现代备用的第一个状态是屏幕处于关闭状态时。 最深的睡眠状态是在 DRIPS/复原能力。 有关详细信息，请参阅[现代待机状态](https://docs.microsoft.com/windows-hardware/design/device-experiences/modern-standby)   |
|KWS                    |关键字 spotter – 提供的"你好，小娜"检测的算法 |
| SW KWS                |软件关键字 spotter – (CPU) 在主机运行的 KWS 的实现。 对于"你好，小娜"SW KWS 是作为 Windows 的一部分。 |
| HW KWS                | 硬件卸载关键字 spotter – 硬件上运行的 KWS 的实现卸载。 |
|突发缓冲区           | 一个循环缓冲区，用于存储可以是 bursted 向上如果 KWS 检测到，以便触发 KWS 检测的所有音频都是包含 PCM 数据。 |
|关键字检测器 OEM 适配器 |启用与 Windows 和 Cortana 堆栈进行通信的启用了 WoV 的 HW 驱动程序级别填充程序。 |
|型号 | 使用 KWS 算法的声学模型，数据文件。 数据文件是静态的。 模型已经过本地化，每个区域设置一个。|

## <a name="span-idimplementingvoiceactivationspanspan-idimplementingvoiceactivationspanspan-idimplementingvoiceactivationspanintegrating-a-hardware-keyword-spotter"></a><span id="Implementing_Voice_Activation"></span><span id="implementing_voice_activation"></span><span id="IMPLEMENTING_VOICE_ACTIVATION"></span>将集成硬件关键字 Spotter

若要实现硬件关键字 spotter (HW KWS) SoC 供应商必须完成以下任务。

-   创建基于本主题后面所述的 SYSVAD 示例自定义关键字检测程序。 将中所述的 COM DLL 中实现这些方法[关键字检测器 OEM 适配器接口](#keyword_detector)。
-   实现批 RT 增强功能中所述[WAVERT 增强功能](#wavert_enhancements)。
-   提供 INF 文件条目来描述用于关键字检测任何自定义 a p o s。
    -   [PKEY\_FX\_KeywordDetector\_StreamEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-keyworddetector-streameffectclsid)
    -   [PKEY\_FX\_KeywordDetector\_ModeEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-keyworddetector-modeeffectclsid)
    -   [PKEY\_FX\_KeywordDetector\_EndpointEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-keyworddetector-endpointeffectclsid)
    -   [PKEY\_SFX\_KeywordDetector\_ProcessingModes\_Supported\_For\_Streaming](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-sfx-keyworddetector-processingmodes-supported-for-streaming)
    -   [PKEY\_MFX\_KeywordDetector\_ProcessingModes\_Supported\_For\_Streaming](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-mfx-keyworddetector-processingmodes-supported-for-streaming)
    -   [PKEY\_EFX\_KeywordDetector\_ProcessingModes\_Supported\_For\_Streaming](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-efx-keyworddetector-processingmodes-supported-for-streaming)
-   查看建议硬件配置和测试中的指导[音频设备建议](https://docs.microsoft.com/windows-hardware/design/component-guidelines/audio)。 本主题提供了指导和建议的设计和开发适用于 Microsoft 的语音平台的音频输入设备。
-   支持同时暂存和命令链接在一起。
-   为每个受支持的 Cortana 区域设置支持"你好，小娜"。 
-   A p o s （音频处理对象） 必须提供以下影响： 
    -   AEC
    -   AGC
    -   NS
-   必须通过 MFX APO 报告语音处理模式的效果。
-   APO 可能执行格式转换为 MFX。   
-   APO 必须输出以下格式： 
    -   16 kHz，mono，FLOAT。
-   （可选） 设计任何自定义不以增强音频捕获进程。 有关详细信息，请参阅[Windows 音频处理对象](windows-audio-processing-objects.md)。

硬件卸载关键字 spotter (HW KWS) WoV 要求
- HW KWS WoV S0 工作状态和 S0 睡眠状态也称为现代待机在受支持。  
- HW KWS WoV 不支持从 S3。  

HW KWS AEC 要求

- Windows 版本 1709
    - 若要支持 S0 HW KWS WoV 睡眠状态 （现代待机） 的 AEC 则不需要。  
    - 在 Windows 版本 1709年中不支持硬件 KWS WoV S0 工作状态。

- Windows 版本 1803 
    - 支持硬件 KWS WoV S0 工作状态。
    - 若要启用 HW KWS WoV 用于 S0 工作状态，请 APO 必须支持 AEC。


## <a name="span-idsamplecodeoverviewspansample-code-overview"></a><span id="sample_code_overview"></span>示例代码概述


没有在 GitHub 作为 SYSVAD 虚拟音频适配器示例的一部分实现语音激活的音频驱动程序的示例代码。 建议使用此代码作为起始点。 在此位置提供了该代码。

<https://github.com/Microsoft/Windows-driver-samples/blob/master/audio/sysvad/>

有关 SYSVAD 示例音频驱动程序的详细信息，请参阅[示例音频驱动程序](sample-audio-drivers.md)。

## <a name="span-idkeywordrecognitionsysteminformationspankeyword-recognition-system-information"></a><span id="keyword_recognition_system_information"></span>关键字识别系统信息


**语音激活音频堆栈支持**

启用语音激活的音频堆栈外部接口作为语音平台和音频驱动程序的通信管道。 外部接口被划分为三个部分中。

-   *关键字检测程序设备驱动程序接口 (DDI)* 。 关键字检测程序设备驱动程序接口负责配置和武装 HW 关键字 Spotter (KWS)。  它还用于驱动程序通知检测事件的系统。
-   *关键字检测器 OEM 适配器 DLL*。 此 DLL 实现 COM 接口，以适应使用由操作系统来帮助进行关键字检测的驱动程序特定不透明数据。
-   *流式处理增强功能的 WaveRT*。 增强功能使音频迸发流缓冲的音频数据驱动程序从关键字检测。

**音频的终结点属性**

音频端点关系图构建通常会发生。 在关系图已准备好比实时捕获更快地处理。 捕获缓冲区上的时间戳保持，则返回 true。 具体而言，时间戳将正确反映在过去和缓冲，捕获和现在"迸发"的数据。

**理论上的操作**

该驱动程序像往常一样公开其捕获设备的 KS 筛选器。 此筛选器支持多个 KS 属性和 KS 事件，用于配置、 启用和信号检测事件。 此筛选器还包括标识为关键字 spotter (KWS) pin 的其他的 pin 工厂。 此 pin 用于流式传输音频从关键字 spotter。

属性包括：

-   支持的关键字类型- [ **KSPROPERTY\_SOUNDDETECTOR\_模式**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-patterns)。 此属性由操作系统设置，若要配置要检测到的关键字。
-   模式的关键字的列表的 Guid- [ **KSPROPERTY\_SOUNDDETECTOR\_SUPPORTEDPATTERNS**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-supportedpatterns)。 此属性用于获取标识的受支持的模式的类型的 Guid 的列表。
-   有- [ **KSPROPERTY\_SOUNDDETECTOR\_ARMED**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-armed)。 此读/写属性是只是布尔值，该值指示是否有检测程序状态。 OS 设置此选项以吸引关键字检测程序。 操作系统可以清除此选项以取消。 该驱动程序会自动清除此设置关键字模式时并且还会在检测到一个关键字。 （OS 必须重置的。）
-   匹配结果- [ **KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-matchresult)。 在发生检测后，此读取的属性保存的结果数据。

如果检测到一个关键字则会激发该事件是[ **KSEVENT\_SOUNDDETECTOR\_MATCHDETECTED** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksevent-sounddetector-matchdetected)事件。

**操作的序列**

*系统启动*

1. 操作系统读取要验证它具有关键字以该格式的受支持的关键字类型。
2. OS 注册检测器状态更改事件。
3. OS 设置关键字模式。
4. 操作系统而检测程序。

*在接收 KS 事件*

1. 该驱动程序 disarms 检测程序。
2. 操作系统读取关键字检测程序状态，分析返回的数据，并确定检测到的模式。
3. OS 重装检测程序。

**内部驱动程序和硬件操作**

了解检测程序，而硬件可连续捕获，且在一个较小的 FIFO 缓冲区中缓冲的音频数据。 （此 FIFO 缓冲区的大小由要求外部本文档中，但通常可能是数百毫秒到数秒钟的时间。）检测算法对通过此缓冲区流式处理的数据进行操作。 驱动程序和硬件的设计是这样，尽管臂此处是驱动程序和硬件并在"应用程序"的处理器不中断之间没有交互，直到检测到一个关键字。 这允许系统达到较低的电源状态，如果没有其他活动。

当硬件检测到一个关键字时，它将生成中断。 在等待服务中断的驱动程序，同时继续到缓冲区中，确保没有数据丢失中缓冲限制, 关键字后捕获音频硬件。

**关键字时间戳**

检测一个关键字后, 所有语音激活解决方案必须都缓冲所有语言关键字，包括开始前的关键字的 250 毫秒。 音频驱动程序必须提供时间戳的开始和结束的流中的关键短语标识。

为了支持关键字开始/结束时间戳，DSP 软件可能需要在内部基于 DSP 时钟的时间戳事件。 一旦检测到一个关键字，与驱动程序以准备 KS 事件进行交互的 DSP 软件。 驱动程序和 DSP 软件将需要将 DSP 时间戳映射到 Windows 性能计数器的值。 执行此操作的方法是特定于硬件设计。 一个可能的解决方案是为要读取 current 性能计数器、 查询当前 DSP 时间戳，同样，读取 current 性能计数器并估计性能计数器和 DSP 时间之间的关联的驱动程序。 然后给定的关联，该驱动程序可以映射关键字 DSP 时间戳到 Windows 性能计数器的时间戳。


## <a name="span-idkeyworddetectorspankeyword-detector-oem-adapter-interface"></a><span id="keyword_detector"></span>关键字检测器 OEM 适配器接口

OEM 提供充当中介，OS 和驱动程序，帮助计算或分析是读取和写入到通过音频驱动程序的不透明数据的 COM 对象实现[ **KSPROPERTY\_SOUNDDETECTOR\_模式**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-patterns)并[ **KSPROPERTY\_SOUNDDETECTOR\_MATCHRESULT**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-matchresult)。

COM 对象的 CLSID 是检测程序模式类型返回的 GUID [ **KSPROPERTY\_SOUNDDETECTOR\_SUPPORTEDPATTERNS**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-supportedpatterns)。 操作系统调用 CoCreateInstance 传递模式类型来实例化与关键字模式类型兼容，该对象的 IKeywordDetectorOemAdapter 接口上调用方法的相应 COM 对象的 GUID。

**COM 线程模型要求**

OEM 的实现可能会选择任何 COM 线程模型。

**IKeywordDetectorOemAdapter**

接口设计会试图保持无状态的对象实现。 换而言之，实现应要求存储方法调用之间没有状态。 事实上，内部C++类可能不需要除一般情况下实现 COM 对象所需之外的所有成员变量。

**方法**

实现以下方法。

-   [**IKeywordDetectorOemAdapter::BuildArmingPatternData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-buildarmingpatterndata)
-   [**IKeywordDetectorOemAdapter::ComputeAndAddUserModelData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-computeandaddusermodeldata)
-   [**IKeywordDetectorOemAdapter::GetCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-getcapabilities)
-   [**IKeywordDetectorOemAdapter::ParseDetectionResultData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-parsedetectionresultdata)
-   [**IKeywordDetectorOemAdapter::VerifyUserKeyword**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-verifyuserkeyword)

**KEYWORDID**

[ **KEYWORDID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/keyworddetectoroemadapter/ne-keyworddetectoroemadapter-__midl_ikeyworddetectoroemadapter_0002)枚举标识关键字短语的文本/函数，还可用于 Windows 生物识别服务适配器中。 有关详细信息，请参阅[生物识别框架概述-核心平台组件](https://docs.microsoft.com/windows/desktop/SecBioMet/biometric-framework-overview)

```cpp
typedef enum  { 
  KwInvalid              = 0,
  KwHeyCortana           = 1,
  KwSelect               = 2
} KEYWORDID;
```

**KEYWORDSELECTOR**

[ **KEYWORDSELECTOR** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/keyworddetectoroemadapter/ns-keyworddetectoroemadapter-__midl_ikeyworddetectoroemadapter_0003)结构是一组唯一选择一种特定的关键字和语言的 Id。

```cpp
typedef struct
{
    KEYWORDID KeywordId;
    LANGID LangId;
} KEYWORDSELECTOR;
```

**处理模型数据**

*静态用户独立模型*-OEM DLL 通常会包含内置到 DLL 或 DLL 中包含的单独的数据文件中的一些静态用户独立模型数据。 受支持的关键字 Id 返回 GetCapabilities 例程集将依赖于此数据。 例如，如果受支持的关键字返回 GetCapabilities 的 Id 列表中包含 KwHeyCortana，静态用户独立模型数据将包括数据适用于"你好，小娜"（或其翻译） 所有支持的语言。

*动态用户依赖模型*-IStream 提供随机访问存储模型。 OS IKeywordDetectorOemAdapter 接口上传递到的许多方法的 IStream 接口指针。 OS 备份最多 1 MB 的数据的 IStream 实现与适当的存储。

由 OEM 定义的内容和此存储中数据的结构。 预期的目的是为了方便永久存储用户依赖模型数据计算或 OEM DLL 来检索。

操作系统可以调用使用的空 IStream 接口方法，尤其是当用户永远不会具有训练一个关键字。 OS 创建单独的 IStream 存储为每个用户。 换而言之，给定的 IStream 存储有且只有一个用户的模型数据。

OEM DLL 开发人员决定如何管理独立于用户和用户相关数据。 但是，它应永远不会存储用户数据的 IStream 之外的任意位置。 一个可能的 OEM DLL 设计会在内部切换访问 IStream 和静态用户独立于数据，具体取决于当前方法的参数。 备用设计可能检查每个方法调用开始处 IStream，并添加静态用户独立数据到 IStream 如果尚不存在，从而允许访问仅模型的所有数据的 IStream 方法的剩余部分。

## <a name="span-idtrainingandoperationaudioprocessingspanspan-idtrainingandoperationaudioprocessingspanspan-idtrainingandoperationaudioprocessingspantraining-and-operation-audio-processing"></a><span id="Training_and_Operation_Audio_Processing"></span><span id="training_and_operation_audio_processing"></span><span id="TRAINING_AND_OPERATION_AUDIO_PROCESSING"></span>培训和操作音频处理


如前面所述，培训 UI 流会导致不可在音频流中的完整发音上丰富句子。 每个句子逐个传递给[ **IKeywordDetectorOemAdapter::VerifyUserKeyword** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-verifyuserkeyword)确认它包含应为的关键字，并且具有可接受的质量。 所有句子是收集并验证通过用户界面后，它们均传递一次调用[ **IKeywordDetectorOemAdapter::ComputeAndAddUserModelData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-computeandaddusermodeldata)。

音频处理语音激活培训的唯一方式。 下表总结了语音激活培训和普通的语音识别使用量之间的差异。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left"><strong>语音训练</strong></td>
<td align="left"><strong>语音识别</strong></td>
</tr>
<tr class="even">
<td align="left"><strong>模式</strong></td>
<td align="left">原始</td>
<td align="left">原始或语音</td>
</tr>
<tr class="odd">
<td align="left"><strong>Pin</strong></td>
<td align="left">正常</td>
<td align="left">KWS</td>
</tr>
<tr class="even">
<td align="left"><strong>音频格式</strong></td>
<td align="left">32 位浮点型 (类型 = 音频，子类型 = IEEE_FLOAT，采样率 = 16 kHz，bits = 32)</td>
<td align="left">由 OS 音频堆栈</td>
</tr>
<tr class="odd">
<td align="left"><strong>Mic</strong></td>
<td align="left">Mic 0</td>
<td align="left">数组或 mono 中的所有接通麦克风</td>
</tr>
</tbody>
</table>



## <a name="span-idkeywordrecognitionsystemoverviewspanspan-idkeywordrecognitionsystemoverviewspanspan-idkeywordrecognitionsystemoverviewspankeyword-recognition-system-overview"></a><span id="Keyword_Recognition_System_Overview"></span><span id="keyword_recognition_system_overview"></span><span id="KEYWORD_RECOGNITION_SYSTEM_OVERVIEW"></span>关键字识别系统概述


此关系图概述了关键字识别系统。

![关键字识别系统包括 cortana 语音运行时和语音激活管理器](images/audio-simple-voice-recon-diagram1.png)

## <a name="span-idkeywordrecognitionsequencediagramsspanspan-idkeywordrecognitionsequencediagramsspanspan-idkeywordrecognitionsequencediagramsspankeyword-recognition-sequence-diagrams"></a><span id="Keyword_Recognition__Sequence_Diagrams"></span><span id="keyword_recognition__sequence_diagrams"></span><span id="KEYWORD_RECOGNITION__SEQUENCE_DIAGRAMS"></span>关键字识别序列图


这些关系图，在"语音平台"显示语音运行时模块。 正如前面提到的例如 Cortana 和听写的 Windows 10 中的所有语音体验的 power 用于 Windows 语音平台。

在启动期间，功能使用收集[ **IKeywordDetectorOemAdapter::GetCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-getcapabilities)。

![在启动期间显示培训语音平台用户体验和 oem 关键字检测器关键字识别序列](images/audio-voice-activation-startup.png)

更高版本时，用户选择"了解我的语音"，调用定型流。

![关键字识别序列显示培训 ux 语音平台和 oem 关键字检测器期间了解我的声音](images/audio-voice-activation-training.png)

下图描述了武装关键字检测的过程。

![关键字识别序列武装关键字检测期间显示语音平台 oem 关键字检测器和音频驱动器检测程序](images/audio-voice-activation-arming.png)

## <a name="span-idwavertenhancementsspanspan-idwavertenhancementsspanspan-idwavertenhancementsspanwavert-enhancements"></a><span id="WAVERT_Enhancements"></span><span id="wavert_enhancements"></span><span id="WAVERT_ENHANCEMENTS"></span>WAVERT 增强功能


微型端口接口定义必须由 WaveRT 微型端口驱动程序。 这些接口提供简化的音频驱动程序，提高 OS 音频管道性能和可靠性，或者支持新方案的方法。 允许驱动程序提供对操作系统的大小限制的其缓冲区静态表达式定义新的即插即用设备接口属性。

**缓冲区大小**

驱动程序将在各种约束下操作时操作系统、 驱动程序和硬件之间移动的音频数据。 这些约束可能是由于内存与硬件之间移动数据的物理硬件传输和/或由于信号处理的硬件或关联的 DSP 中的模块。

HW KWS 解决方案必须支持音频捕获大小至少 100 毫秒的和最多 200 毫秒。

该驱动程序表明自己获得缓冲区大小限制，通过设置 DEVPKEY\_KsAudio\_PacketSize\_KSCATEGORY 约束设备属性\_具有 KS KS 筛选器的音频即插即用设备接口流式处理 pin(s)。 此属性应保持有效且稳定，而启用 KS 筛选器接口。 而无需打开的句柄驱动程序和驱动程序上调用，操作系统可以随时读取此值。

**DEVPKEY\_KsAudio\_PacketSize\_Constraints**

DEVPKEY\_KsAudio\_PacketSize\_约束属性值包含[ **KSAUDIO\_PACKETSIZE\_约束**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints)结构的结构描述 （即由于将数据从 WaveRT 缓冲区传输到音频硬件的机制） 的物理硬件约束。 结构包含一系列的 0 或更多[ **KSAUDIO\_PACKETSIZE\_PROCESSINGMODE\_约束**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksaudio_packetsize_signalprocessingmode_constraint)结构描述特定于任何约束信号处理模式。 驱动程序设置此属性之前调用[ **PcRegisterSubdevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregistersubdevice)或否则启用其流式处理插针，其 KS 筛选器接口。

**IMiniportWaveRTInputStream**

驱动程序实现此接口的音频数据流从驱动程序到操作系统的更好地协调。 如果此接口上捕获流不可用，操作系统将使用此接口上的方法来访问 WaveRT 缓冲区中的数据。 有关详细信息，请参阅[ **IMiniportWaveRTInputStream::GetReadPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket)

**IMiniportWaveRTOutputStream**

WaveRT 微型端口根据需要实现此接口可以收到通知的 OS 从写入进度，并返回精确的流位置。 有关详细信息请参阅[ **IMiniportWaveRTOutputStream::SetWritePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavertoutputstream-setwritepacket)， [ **IMiniportWaveRTOutputStream::GetOutputStreamPresentationPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavertoutputstream-getoutputstreampresentationposition)并[ **IMiniportWaveRTOutputStream::GetPacketCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavertoutputstream-getpacketcount)。

**性能计数器的时间戳**

多个驱动程序例程返回专用于反映将的时间示例是捕获或该设备提供的 Windows 性能计数器时间戳。

设备具有复杂 DSP 中的管道和信号处理，计算准确的时间戳可能具挑战性，并且应经过深思熟虑。 时间戳不应只是反映在该示例已传输到或从操作系统到 DSP 的时间。

-   内 DSP，跟踪示例使用某些内部的 DSP 时钟的时间戳。
-   驱动程序和 DSP，计算的 Windows 性能计数器和 DSP 时钟之间的相关性。 此过程的范围可以从非常简单 （但不太精确） 到相当复杂的或新颖 （但更精确的）。
-   除非这些延迟否则实现考虑进来由于信号处理算法或管道或硬件传输任何常量的延迟。

**突发读取操作**

本部分介绍对迸发读取的 OS 和驱动程序交互。 突发读取可能发生语音激活方案之外，只要该驱动程序支持基于数据包流 WaveRT 模型，包括[ **IMiniportWaveRTInputStream::GetReadPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket)函数。

两个突发示例读取讨论这些方案。 在一个方案中，如果微型端口支持具有 pin 类别 pin [ **KSNODETYPE\_音频\_KEYWORDDETECTOR** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-audio-keyworddetector)然后，该驱动程序将开始捕获，并在内部缓冲的数据时检测到一个关键字。 在另一个方案中，该驱动程序可以根据需要在内部缓冲 WaveRT 缓冲区外的数据如果 OS 不读取数据足够快的速度通过调用[ **IMiniportWaveRTInputStream::GetReadPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket).

在过渡到 KSSTATE 之前捕获的迸发数据\_运行，该驱动程序必须保留以及缓冲的捕获的数据的准确示例时间戳信息。 时间戳识别采样即时捕获示例。

1. 之后，将流转换为 KSSTATE\_运行，该驱动程序立即设置缓冲区通知事件因为它已有可用的数据。
2. 在此情况下，OS 将调用 GetReadPacket() 以获取有关可用数据的信息。

    a. 驱动程序将返回有效的捕获数据的数据包数 (0 表示从 KSSTATE 转换后的第一个数据包\_停止到 KSSTATE\_运行)，操作系统可以从其派生 WaveRT 缓冲区，以及数据包中的数据包位置相对于流的开始位置。

    b. 驱动程序还返回采样的性能计数器的值相对应的即时的数据包中的第一个示例。 请注意，此性能计数器的值可能是相对较旧，具体取决于捕获的数据量已缓冲中的硬件或驱动程序 （在外部 WaveRT 缓冲区）。

    c. 如果没有更多未读缓冲的数据可用驱动程序或者： 我。 立即传输到 WaveRT 缓冲区 （即未使用的空间 GetReadPacket 从返回的数据包），可用空间数据为 MoreData，返回 true，并在该例程中返回前设置缓冲区通知事件。 或者，ii。 程序硬件迸发到 WaveRT 缓冲区的可用空间的下一个数据包 MoreData，返回 false 和更高版本设置时在传输完成的缓冲事件。
3. 操作系统从使用 GetReadPacket() 返回的信息 WaveRT 缓冲区中读取数据。
4. 操作系统将等待下一个缓冲区通知事件。 如果该驱动程序步骤 (2 c) 中设置缓冲区通知，在等待可能会立即终止。
5. 如果该驱动程序未立即设置在步骤 (2 c) 事件，该驱动程序设置后它将捕获更多的数据传输到 WaveRT 缓冲区并使其可供操作系统读取的事件
6. 请转到 (2)。
有关[ **KSNODETYPE\_音频\_KEYWORDDETECTOR** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-audio-keyworddetector)关键字检测器插针，驱动程序应该分配至少 5000 ms 的音频数据足够内部迸发缓冲。 如果操作系统无法创建 pin 之前的缓冲区溢出然后驱动程序上的流可能最终的内部缓冲的活动和关联的免费资源。


## <a name="span-idwakeonvoicespanspan-idwakeonvoicespanspan-idwakeonvoicespanwake-on-voice"></a><span id="Wake_on_Voice"></span><span id="wake_on_voice"></span><span id="WAKE_ON_VOICE"></span>唤醒语音

唤醒上语音 (WoV) 使用户能够激活和查询向屏幕上，通过说出特定关键字，如"你好，小娜"完整的电源状态从屏幕关闭节能状态，语音识别引擎。

此功能允许设备在低功耗状态，包括屏幕处于关闭状态，并在设备处于空闲状态时在设备处于时始终侦听用户的语音。 使用侦听模式，这是较低电源时相比更高版本电源使用量在正常的麦克风录制过程中所示执行此操作。 低能耗语音识别，用户只需说"你好，小娜"后, 跟链接的语音短语等预定义的关键短语喜欢"时是我下一步的约会"无需手动方式调用语音。 这将正常工作而不考虑设备是否正在使用中或屏幕空闲关闭。

音频堆栈负责通信唤醒数据 （演讲者 ID、 关键字触发器，置信度级别） 以及通知相关客户端检测到关键字。


## <a name="span-idwovvalidationspanspan-idwovvalidationspanspan-idwovvalidationspan-validation-on-modern-standby-systems"></a><span id="WOV_Validation"></span><span id="wov_validation"></span><span id="WOV_VALIDATION"></span> 新式的备用系统上的验证

从系统空闲状态的 WoV 可以验证上[现代待机](https://docs.microsoft.com/windows-hardware/design/device-experiences/modern-standby)使用的系统[待机状态唤醒语音交流电源源上的基本测试的现代](https://docs.microsoft.com/windows-hardware/test/hlk/testref/69df7cf2-6024-4eee-92ee-1506480614ee)和[待机状态唤醒语音基本测试的现代在 DC 电源](https://docs.microsoft.com/windows-hardware/test/hlk/testref/614ffb93-eced-45ab-bf7b-e09291a97fd2)中[HLK](https://docs.microsoft.com/windows-hardware/test/hlk/)。 这些测试检查系统具有硬件关键字 spotter (HW KWS)，可以输入最深的运行时空闲平台状态 (DRIPS) 以及能够从现代待机状态唤醒语音命令，且系统恢复滞后时间为小于或等于 1 秒。 