---
title: 语音激活
description: Cortana，Windows 语音平台用于为 Windows 10 中的所有语音体验（例如 Cortana 和听写）供电。
ms.assetid: 0684EF32-AA76-418B-9027-1C067A8140E3
ms.date: 05/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: 797b27baa8aa4f6fb4208c170ec45fd19e46d68a
ms.sourcegitcommit: a391539e144ffc610db9eec05875568c72878eb2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85854459"
---
# <a name="voice-activation"></a>语音激活

> [!NOTE]
> 本主题主要涉及我们在 Windows 10 （版本1909及更早版本）中提供的使用者体验。

Cortana，在2013中的 Microsoft BUILD 开发人员大会首次演示了个人助手技术。 Windows 语音平台用于为 Windows 10 中的所有语音体验（例如 Cortana 和听写）供电。 语音激活是一项功能，使用户能够通过口述特定短语 "你好 Cortana" 从各种设备电源状态调用语音识别引擎。 若要创建支持语音激活技术的硬件，请查看本主题中的信息。

> [!NOTE]
> 实现语音激活是一种重要的项目，是由 SoC 供应商完成的任务。 Oem 可以联系其 SoC 供应商，了解有关其 SoC 的语音激活实现的信息。

## <a name="cortana-end-user-experience"></a>Cortana 最终用户体验

若要了解 Windows 中可用的语音交互体验，请查看以下主题。

|主题|说明|
|----|----|
| [什么是 Cortana？](https://support.microsoft.com/help/17214/cortana-what-is)      | 提供 Cortana 的概述和使用方向                 |
| [使 Cortana 彰显你的个性](https://support.microsoft.com/help/17178/windows-10-make-cortana-yours) | 描述可通过 Cortana 的 "设置" 屏幕进行的自定义。 |

## <a name="introduction-to-hey-cortana-voice-activation-and-learn-my-voice"></a>"你好 Cortana" 语音激活和 "了解我的语音" 简介

### <a name="hey-cortana-voice-activation"></a>你好 Cortana "语音激活

使用 "你好 Cortana" 语音激活（VA）功能，用户可以通过语音在活动上下文之外（即，当前在屏幕上）快速进行 Cortana 体验。 用户经常希望能够立即访问体验，而无需对设备进行物理交互。 对于电话用户，这可能是因为在汽车中推动并密切关注运营车。 对于 Xbox 用户，这可能是由于找不到并连接控制器。 对于 PC 用户，这可能是因为快速访问体验，而无需执行多个鼠标、触控和/或键盘操作，例如厨房中的计算机。

语音激活提供始终通过预定义的关键短语或 "激活短语" 来侦听语音输入。 关键短语可能会自行失措（"你好 Cortana"）作为暂存命令，也可后跟语音操作，例如，"你好 Cortana，其中是下一会议？"，它是一个链式命令。

术语 "*关键字检测*" 描述硬件或软件对关键字的检测。

*仅限关键字*激活当只提到 cortana 关键字时，Cortana 会启动并播放 EarCon 声音，以指示它已进入侦听模式。

*链式命令*描述了发出紧跟关键字后面的命令（如 "你好 Cortana，call John"）并让 Cortana 启动（如果尚未启动）并遵循命令（开始与 John 进行电话呼叫）的功能。

此图说明了链式和关键字的激活。

![显示音频缓冲区和时间序列的链接和关键字激活关系图](images/audio-chained-keyword-activation.png)

Microsoft 提供了 OS default 关键字 spotter （software 关键字 spotter），用于确保硬件关键字检测的质量，并在硬件关键字检测缺少或不可用的情况下提供 "你好 Cortana" 体验。

### <a name="the-learn-my-voice-feature"></a>"了解我的语音" 功能

"了解我的语音" 功能允许用户训练 Cortana 来识别其独特的声音。 这是通过用户单击 "Cortana 设置" 屏幕上的 *"使用 cortana"* 来完成的。 然后，用户重复六个经过认真选择的短语，该短语提供了丰富的各种拼音模式来标识用户语音的唯一属性。

![适用于 hw 的 cortana 桌面设置关键字 spotter 唤醒](images/audio-voice-activation-settings-2017.png)

当语音激活与 "了解我的语音" 配对时，这两种算法将协同工作以减少错误激活。 这对于会议室方案特别有用，其中一个人在设备上显示 "你好 Cortana"。 此功能仅适用于 Windows 10 版本1903及更早版本。

语音激活由关键字 spotter （KWS）提供支持，它会响应是否检测到密钥短语。 如果 KWS 将设备从 "低" 状态唤醒，则此解决方案称为 "语音唤醒" （WoV）。 有关详细信息，请参阅[唤醒](#wake-on-voice)。

## <a name="glossary-of-terms"></a>术语词汇表

此词汇表汇总了与语音激活相关的术语。

|术语|示例/定义|
|----|----|
| 暂存命令        | 示例：你好，Cortana <暂停，> 天气情况下等待 earcon？ 这有时称为 "双拍命令" 或 "仅限关键字" |
|链式命令        | 示例：您好 Cortana 的天气是什么？ 这有时称为 "一次" 命令 |
| 语音激活      | 提供预定义激活关键短语关键字检测的方案。 例如，"你好 Cortana" 是 Microsoft 语音激活方案。 |
|WoV                    | 唤醒-语音-从屏幕关闭语音激活，将电源状态降低到处于完全供电状态的屏幕。 |
|从新式备用 WoV| 从新式备用（S0ix）屏幕关闭状态到屏幕上的完全电源（S0）状态唤醒。 |
|新式待机 |Windows 低功耗空闲基础结构-Windows 10 中连接备用（CS）的后续版本。 新式备用的第一种状态是在屏幕关闭时。 最深层睡眠状态是在 DRIPS/复原中。 有关详细信息，请参阅[新式备用](https://docs.microsoft.com/windows-hardware/design/device-experiences/modern-standby)   |
|KWS                    |关键字 spotter –提供 "你好 Cortana" 检测的算法 |
| SW KWS                |Software 关键字 spotter –主机（CPU）上运行的 KWS 的实现。 对于 "你好 Cortana"，软件 KWS 包含在 Windows 中。 |
| HW KWS                | 硬件卸载关键字 spotter –在硬件上运行的 KWS 的实现。 |
|突发缓冲区           | 一种用于存储在 KWS 检测时可以 "bursted" 的 PCM 数据的循环缓冲区，因此包括触发 KWS 检测的所有音频。 |
|关键字检测器 OEM 适配器 |一种驱动程序级别填充程序，使支持 WoV 的 HW 能够与 Windows 和 Cortana 堆栈进行通信。 |
|型号 | KWS 算法使用的声音模型数据文件。 数据文件为静态。 模型已本地化，每个区域设置一个。|

## <a name="integrating-a-hardware-keyword-spotter"></a>集成硬件关键字 Spotter

若要实现硬件关键字 spotter （HW KWS） SoC 供应商，必须完成以下任务。

- 根据本主题后面所述的 SYSVAD 示例创建自定义关键字检测器。 你将在 COM DLL 中实现这些方法，如[关键字检测器 OEM 适配器接口](#keyword-detector-oem-adapter-interface)中所述。
- 实现[WAVERT 增强](#wavert-enhancements)中所述的声波 RT 增强功能。
- 提供 INF 文件项来描述用于关键字检测的任何自定义项。
  - [PKEY \_ FX \_ KeywordDetector \_ StreamEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-keyworddetector-streameffectclsid)
  - [PKEY \_ FX \_ KeywordDetector \_ ModeEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-keyworddetector-modeeffectclsid)
  - [PKEY \_ FX \_ KeywordDetector \_ EndpointEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-keyworddetector-endpointeffectclsid)
  - [PKEY \_ SFX \_ KeywordDetector \_ ProcessingModes \_ 支持 \_ \_ 流式处理](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-sfx-keyworddetector-processingmodes-supported-for-streaming)
  - [PKEY \_ MFX \_ KeywordDetector \_ ProcessingModes \_ 支持 \_ \_ 流式处理](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-mfx-keyworddetector-processingmodes-supported-for-streaming)
  - [PKEY \_ EFX \_ KeywordDetector \_ ProcessingModes \_ 支持 \_ \_ 流式处理](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-efx-keyworddetector-processingmodes-supported-for-streaming)
- 在[音频设备建议](https://docs.microsoft.com/windows-hardware/design/component-guidelines/audio)中查看硬件建议和测试指南。 本主题提供用于设计和开发用于 Microsoft 语音平台的音频输入设备的指南和建议。
- 支持暂存和链式命令。
- 支持每个受支持 Cortana 区域设置的 "你好 Cortana"。
- 中（音频处理对象）必须提供以下效果：
  - AEC
  - AGC
  - NS
- 语音处理模式的效果必须由 MFX APO 报告。
- APO 可以将格式转换作为 MFX 执行。
- APO 必须输出以下格式：
  - 16 kHz，mono，FLOAT。
- 选择性地设计任何自定义的，以增强音频捕获过程。 有关详细信息，请参阅[Windows 音频处理对象](windows-audio-processing-objects.md)。

硬件卸载关键字 spotter （HW KWS） WoV 要求

- 在 S0 工作状态和 S0 睡眠状态也称为新式备用时，支持 HW KWS WoV。  
- S3 不支持 HW KWS WoV。  

HW KWS 的 AEC 要求

- 对于 Windows 版本1709
  - 不需要支持 HW KWS WoV for S0 睡眠状态（新式备用） AEC。  
  - Windows 版本1709不支持适用于 S0 工作状态的 HW KWS WoV。

- 对于 Windows 版本1803
  - HW KWS WoV 支持 S0 工作状态。
  - 若要启用 HW KWS WoV for S0 工作状态，APO 必须支持 AEC。

## <a name="sample-code-overview"></a>示例代码概述

在 GitHub 上实现语音激活的音频驱动程序的示例代码是 SYSVAD 虚拟音频适配器示例的一部分。 建议使用此代码作为起点。 此位置提供了代码。

<https://github.com/Microsoft/Windows-driver-samples/blob/master/audio/sysvad/>

有关 SYSVAD 示例音频驱动程序的详细信息，请参阅[示例音频驱动程序](sample-audio-drivers.md)。

## <a name="keyword-recognition-system-information"></a>关键字识别系统信息

### <a name="voice-activation-audio-stack-support"></a>语音激活音频堆栈支持

用于启用语音激活的音频堆栈外部接口用作语音平台和音频驱动程序的通信管道。 外部接口分为三部分。

- *关键字检测器设备驱动程序接口（DDI）*。 关键字检测器设备驱动程序接口负责配置和武装 HW 关键字 Spotter （KWS）。  它还可由驱动程序用来通知系统检测事件。
- *关键字检测器 OEM 适配器 DLL*。 此 DLL 实现了一个 COM 接口，用于改编驱动程序特定的不透明数据以供 OS 用于帮助进行关键字检测。
- *WaveRT 流增强功能*。 增强功能使得音频驱动程序能够突发地流式传输来自关键字检测的缓冲音频数据。

### <a name="audio-endpoint-properties"></a>音频终结点属性

音频终结点图形生成正常。 该图形准备处理的速度比实时捕获更快。 捕获的缓冲区上的时间戳始终为 true。 具体而言，时间戳会正确反映过去和缓冲时捕获的数据，现在为 "突发"。

### <a name="theory-of-operation"></a>操作理论

驱动程序会像往常一样为其捕获设备公开 KS 筛选器。 此筛选器支持多个 KS 属性和一个 KS 事件来配置、启用和发出检测事件信号。 此筛选器还包括一个标识为关键字 spotter （KWS） pin 的附加 pin 工厂。 此 pin 用于从关键字 spotter 流式传输音频。

这些属性为：

- 支持的关键字类型- [**KSPROPERTY \_ SOUNDDETECTOR \_ 模式**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-patterns)。 此属性由操作系统设置，用于配置要检测的关键字。
- 关键字模式 Guid 列表- [**KSPROPERTY \_ SOUNDDETECTOR \_ SUPPORTEDPATTERNS**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-supportedpatterns)。 此属性用于获取 Guid 列表，这些 Guid 用于标识支持模式的类型。
- [**KSPROPERTY \_ SOUNDDETECTOR \_ **](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-armed)。 此读取/写入属性是一个简单的布尔状态，它指示是否已确定探测器。 操作系统将此设置为参与关键字检测器。 操作系统可以清除此来脱开。 如果设置了关键字模式，并且在检测到了关键字之后，驱动程序会自动清除此设置。 （操作系统必须进行重置。）
- Match result- [**KSPROPERTY \_ SOUNDDETECTOR \_ MATCHRESULT**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-matchresult)。 此 read 属性保存检测后的结果数据。

检测到关键字时触发的事件是一个[**KSEVENT \_ SOUNDDETECTOR \_ MATCHDETECTED**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksevent-sounddetector-matchdetected)事件。

### <a name="sequence-of-operation"></a>操作顺序

#### <a name="system-startup"></a>系统启动

1. 操作系统读取受支持的关键字类型，以验证它是否具有该格式的关键字。
2. OS 注册检测程序状态更改事件。
3. OS 设置关键字模式。
4. 操作系统会对检测到探测器。

#### <a name="on-receiving-the-ks-event"></a>收到 KS 事件时

1. 驱动程序 disarms。
2. 操作系统读取关键字检测器状态，分析返回的数据，并确定检测到的模式。
3. OS rearms 检测。

### <a name="internal-driver-and-hardware-operation"></a>内部驱动程序和硬件操作

尽管检测到了探测器，但硬件可以在小型 FIFO 缓冲区中持续捕获和缓冲音频数据。 （此 FIFO 缓冲区的大小由本文档之外的要求确定，但通常为数百毫秒到几秒钟。）检测算法通过此缓冲区对数据流进行操作。 驱动程序和硬件的设计是这样的，尽管在检测到关键字之前，驱动程序与硬件之间没有任何交互，也不会中断到 "应用程序" 处理器。 这允许系统在没有其他活动的情况下接通电源状态。

当硬件检测到某个关键字时，它会生成一个中断。 在等待驱动程序为中断提供服务的同时，硬件将继续将音频捕获到缓冲区中，并确保关键字在超过缓冲限制的情况下不会丢失任何数据。

### <a name="keyword-timestamps"></a>关键字时间戳

在检测关键字之后，所有语音激活解决方案都必须缓冲所有口述关键字，包括关键字开头之前的250毫秒。 音频驱动程序必须提供标识流中关键短语的开始和结束时间的时间戳。

为了支持关键字的开始/结束时间戳，DSP 软件可能需要基于 DSP 时钟的内部时间戳事件。 一旦检测到了某个关键字，DSP 软件就会与该驱动程序交互以准备 KS 事件。 驱动程序和 DSP 软件需要将 DSP 时间戳映射到 Windows 性能计数器值。 执行此操作的方法特定于硬件设计。 一种可能的解决方案是，驱动程序读取当前性能计数器、查询当前 DSP 时间戳、再次读取当前性能计数器，然后估计性能计数器和 DSP 时间之间的相关性。 然后，根据相关关系，驱动程序可以将关键字 DSP 时间戳映射到 Windows 性能计数器时间戳。

## <a name="keyword-detector-oem-adapter-interface"></a>关键字检测器 OEM 适配器接口

OEM 提供一个 COM 对象实现，它充当 OS 和驱动程序之间的中介，有助于计算或分析通过[**KSPROPERTY \_ SOUNDDETECTOR \_ 模式**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-patterns)和[**KSPROPERTY \_ SOUNDDETECTOR \_ MATCHRESULT**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-matchresult)写入和读取到音频驱动程序的不透明数据。

COM 对象的 CLSID 是由[**KSPROPERTY \_ SOUNDDETECTOR \_ SUPPORTEDPATTERNS**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-sounddetector-supportedpatterns)返回的探测器模式类型 GUID。 OS 调用 CoCreateInstance，传递模式类型 GUID 来实例化与关键字模式类型兼容的适当 COM 对象，并调用对象的 IKeywordDetectorOemAdapter 接口上的方法。

### <a name="com-threading-model-requirements"></a>COM 线程模型要求

OEM 的实现可以选择任何 COM 线程模型。

### <a name="ikeyworddetectoroemadapter"></a>IKeywordDetectorOemAdapter

接口设计会尝试使对象实现保持无状态。 换句话说，实现应要求在方法调用之间不存储任何状态。 事实上，内部 c + + 类可能不需要除实现 COM 对象所需的所有成员变量。

### <a name="methods"></a>方法

实现以下方法。

- [**IKeywordDetectorOemAdapter::BuildArmingPatternData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-buildarmingpatterndata)
- [**IKeywordDetectorOemAdapter::ComputeAndAddUserModelData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-computeandaddusermodeldata)
- [**IKeywordDetectorOemAdapter：： GetCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-getcapabilities)
- [**IKeywordDetectorOemAdapter：:P arseDetectionResultData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-parsedetectionresultdata)
- [**IKeywordDetectorOemAdapter::VerifyUserKeyword**](https://docs.microsoft.com/windows-hardware/drivers/ddi/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-verifyuserkeyword)

### <a name="keywordid"></a>KEYWORDID

[**KEYWORDID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/keyworddetectoroemadapter/ne-keyworddetectoroemadapter-__midl_ikeyworddetectoroemadapter_0002)枚举标识关键字的短语文本/函数，还用于 Windows 生物识别服务适配器。 有关详细信息，请参阅[生物识别框架概述-核心平台组件](https://docs.microsoft.com/windows/desktop/SecBioMet/biometric-framework-overview)

```cpp
typedef enum  {
  KwInvalid              = 0,
  KwHeyCortana           = 1,
  KwSelect               = 2
} KEYWORDID;
```

### <a name="keywordselector"></a>KEYWORDSELECTOR

[**KEYWORDSELECTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/keyworddetectoroemadapter/ns-keyworddetectoroemadapter-__midl_ikeyworddetectoroemadapter_0003)结构是一组用于唯一选择特定关键字和语言的 id。

```cpp
typedef struct
{
    KEYWORDID KeywordId;
    LANGID LangId;
} KEYWORDSELECTOR;
```

### <a name="handling-model-data"></a>处理模型数据

*静态用户独立模式*-OEM DLL 通常包含某些内置于 dll 中或包含在 dll 中的单独数据文件中的静态用户独立模型数据。 GetCapabilities 例程返回的支持的关键字 Id 集将取决于此数据。 例如，如果 GetCapabilities 返回的支持的关键字 Id 列表包括 KwHeyCortana，则静态用户独立模型数据将包含所有支持语言的 "你好 Cortana" （或其转换）的数据。

*动态用户相关模型*-IStream 提供随机访问存储模型。 操作系统将一个 IStream 接口指针传递到 IKeywordDetectorOemAdapter 接口上的许多方法。 操作系统可为 IStream 实现提供适当的存储空间，最多支持1MB 的数据。

此存储中的数据的内容和结构由 OEM 定义。 预期目的是通过 OEM DLL 计算或检索的用户相关模型数据的持久存储。

OS 可能使用空的 IStream 调用接口方法，特别是在用户从未定型过关键字的情况下。 操作系统为每个用户创建单独的 IStream 存储。 换句话说，给定的 IStream 将为一个用户和仅一个用户存储模型数据。

OEM DLL 开发人员决定如何管理独立于用户的数据和用户相关数据。 但是，它绝不应将用户数据存储在 IStream 之外的任何位置。 根据当前方法的参数，可能会在内部根据当前方法的参数，在访问 IStream 和静态用户无关数据之间进行切换。 备用设计可在每个方法调用开始时检查 IStream，并将静态用户独立数据添加到 IStream （如果尚未存在），从而使其他方法只能访问所有模型数据的 IStream。

## <a name="training-and-operation-audio-processing"></a>培训和操作音频处理

正如前文所述，定型 UI 流会导致在音频流中提供完整的发音丰富的句子。 每个句子单独传递到[**IKeywordDetectorOemAdapter：： VerifyUserKeyword**](https://docs.microsoft.com/windows-hardware/drivers/ddi/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-verifyuserkeyword) ，以验证它是否包含预期关键字并且具有可接受的质量。 UI 收集并验证所有句子后，所有句子都将通过一次调用传递到[**IKeywordDetectorOemAdapter：： ComputeAndAddUserModelData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-computeandaddusermodeldata)。

音频以独特方式处理语音激活培训。 下表总结了语音激活培训与常规语音识别使用情况之间的区别。

|<table>
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
<td align="left">Raw 或语音</td>
</tr>
<tr class="odd">
<td align="left"><strong>引脚</strong></td>
<td align="left">普通</td>
<td align="left">KWS</td>
</tr>
<tr class="even">
<td align="left"><strong>音频格式</strong></td>
<td align="left">32位 float （类型 = 音频，子类型 = IEEE_FLOAT，采样率 = 16 kHz，位 = 32）</td>
<td align="left">由 OS 音频堆栈管理</td>
</tr>
<tr class="odd">
<td align="left"><strong>In</strong></td>
<td align="left">Mic 0</td>
<td align="left">数组中的所有 mic 或 mono</td>
</tr>
</tbody>
</table>

## <a name="keyword-recognition-system-overview"></a>关键字识别系统概述

此图提供关键字识别系统的概述。

![关键字识别系统，包括 cortana 和语音激活管理器](images/audio-simple-voice-recon-diagram1.png)

## <a name="keyword-recognition-sequence-diagrams"></a>关键字识别顺序关系图

在这些关系图中，语音运行时模块显示为 "语音平台"。 如前所述，Windows 语音平台用于为 Windows 10 中的所有语音体验（例如 Cortana 和听写）供电。

在启动过程中，将使用[**IKeywordDetectorOemAdapter：： GetCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/keyworddetectoroemadapter/nf-keyworddetectoroemadapter-ikeyworddetectoroemadapter-getcapabilities)收集功能。

![关键字识别顺序，显示在启动过程中训练 ux 语音平台和 oem 关键字检测器](images/audio-voice-activation-startup.png)

以后当用户选择 "了解我的语音" 时，将调用训练流。

![关键字识别顺序显示训练 ux 语音平台和 oem 关键字检测器了解语音](images/audio-voice-activation-training.png)

此图描述了武装 for 关键字检测过程。

![关键字识别顺序，显示语音平台 oem 关键字检测器和武装 for 关键字检测期间的音频驱动器探测器](images/audio-voice-activation-arming.png)

## <a name="wavert-enhancements"></a>WAVERT 增强功能

小型端口接口定义为由 WaveRT 微型端口驱动程序实现。 这些接口提供了简化音频驱动程序的方法，改进了 OS 音频管道的性能和可靠性，或支持新的方案。 定义了一个新的 PnP 设备接口属性，该属性允许驱动程序向操作系统提供其缓冲区大小约束的静态表达式。

### <a name="buffer-sizes"></a>缓冲区大小

在操作系统、驱动程序和硬件之间移动音频数据时，驱动程序在各种约束下运行。 这些限制可能是由于物理硬件传输在内存和硬件间移动数据，以及/或者由于硬件或关联的 DSP 中的信号处理模块导致的。

硬件-KWS 解决方案至少必须支持100ms 和200毫秒的音频捕获大小。

驱动程序通过在 \_ \_ \_ \_ 包含 ks 流式处理 pin 的 KS 筛选器的 KSCATEGORY 音频 PnP 设备接口上设置 DEVPKEY KsAudio PacketSize 约束设备属性来表示缓冲区大小约束。 当启用了 KS 筛选器接口时，此属性应保持有效且稳定。 操作系统可以随时读取此值，而无需打开驱动程序的句柄并对驱动程序调用。

### <a name="devpkey_ksaudio_packetsize_constraints"></a>DEVPKEY \_ KsAudio \_ PacketSize \_ 约束

DEVPKEY \_ KsAudio \_ PacketSize \_ 约束属性值包含一个[**KsAudio \_ PacketSize \_ 约束**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints)结构，该结构描述物理硬件约束（例如，由于将数据从 WaveRT 缓冲区传输到音频硬件的机制）。 此结构包含一个数组，其中包含0个或多个[**KSAUDIO \_ PACKETSIZE \_ PROCESSINGMODE \_ 约束**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_signalprocessingmode_constraint)结构，其中描述了特定于任何信号处理模式的约束。 驱动程序在调用[**PcRegisterSubdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregistersubdevice)之前设置此属性，或以其他方式为其流式处理 pin 启用其 KS 筛选器接口。

### <a name="iminiportwavertinputstream"></a>IMiniportWaveRTInputStream

驱动程序实现此接口，以便更好地协调从驱动程序到操作系统的音频数据流。 如果此接口在捕获流中可用，则操作系统将使用此接口上的方法访问 WaveRT 缓冲区中的数据。 有关详细信息，请参阅[ **IMiniportWaveRTInputStream：： GetReadPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket)

### <a name="iminiportwavertoutputstream"></a>IMiniportWaveRTOutputStream

WaveRT 微型端口可以选择实现此接口，以便建议从 OS 写入进度并返回准确的流位置。 有关详细信息，请参阅[**IMiniportWaveRTOutputStream：： SetWritePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertoutputstream-setwritepacket)、 [**IMiniportWaveRTOutputStream：： GetOutputStreamPresentationPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertoutputstream-getoutputstreampresentationposition)和[**IMiniportWaveRTOutputStream：： GetPacketCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertoutputstream-getpacketcount)。

### <a name="performance-counter-timestamps"></a>性能计数器时间戳

几个驱动程序例程返回 Windows 性能计数器时间戳，反映设备捕获或显示样本的时间。

在具有复杂的 DSP 管道和信号处理的设备中，计算准确的时间戳可能会很困难，应周全完成。 时间戳不应简单地反映从 OS 向 DSP 传输样本的时间。

- 在 DSP 内，使用某种内部的 DSP 墙壁跟踪示例时间戳。
- 在驱动程序和 DSP 之间，计算 Windows 性能计数器和 DSP 墙壁时钟之间的关联。 此过程的过程包括非常简单（但不精确）到相当复杂或 novel （但更精确）。
- 由于信号处理算法、管道或硬件传输而导致的任何常量延迟，除非其他情况下会考虑这些延迟。

### <a name="burst-read-operation"></a>突发读取操作

本部分介绍了突发读取的操作系统和驱动程序交互。 只要驱动程序支持基于数据包的流式处理 WaveRT 模型（包括[**IMiniportWaveRTInputStream：： GetReadPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket)函数），就可以在语音激活方案之外执行突发读取。

讨论了两次突发示例读取方案。 在一种方案中，如果微型端口支持 pin 类别为[**KSNODETYPE \_ AUDIO \_ KEYWORDDETECTOR**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-audio-keyworddetector)的 pin，则在检测到关键字时，驱动程序将开始捕获和内部缓冲数据。 在另一种情况下，如果 OS 不是通过调用[**IMiniportWaveRTInputStream：： GetReadPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket)更快地读取数据，则驱动程序可以有选择地在 WaveRT 缓冲区之外缓冲数据。

若要突发在转换到 KSSTATE 运行之前捕获的数据 \_ ，驱动程序必须保留准确的示例时间戳信息以及缓冲捕获数据。 时间戳标识捕获样本的即时采样。

1. 流过渡到 KSSTATE 运行后 \_ ，该驱动程序会立即设置缓冲区通知事件，因为它已经有可用数据。
2. 在此事件中，操作系统将调用 GetReadPacket （）来获取有关可用数据的信息。

    a. 驱动程序将返回有效捕获的数据（0表示从 KSSTATE STOP 转换到 KSSTATE 运行后的第一个数据包）的数据包号 \_ \_ ，操作系统可从该数据派生 WaveRT 缓冲区内的数据包位置以及相对于流开始的数据包位置。

    b. 驱动程序还会返回性能计数器值，该值对应于数据包中第一个样本的采样瞬时。 请注意，此性能计数器值可能相对较旧，这取决于在硬件或驱动程序（WaveRT 缓冲区之外）缓冲捕获数据的程度。

    c. 如果有更多未读缓冲数据可用，则为： i。 立即将此数据传输到 WaveRT 缓冲区的可用空间（即，未由 GetReadPacket 返回的数据包使用的空间），对 MoreData 返回 true，并在从该例程返回之前设置缓冲区通知事件。 或 ii。 计划硬件将下一个数据包传输到 WaveRT 缓冲区的可用空间中，为 MoreData 返回 false，并在传输完成时设置 buffer 事件。
3. 操作系统使用 GetReadPacket （）返回的信息从 WaveRT 缓冲区读取数据。
4. OS 等待下一个缓冲区通知事件。 如果驱动程序在步骤中设置了缓冲区通知，等待可能会立即终止。
5. 如果驱动程序没有在步骤（2c）中立即设置事件，则驱动程序会在将更多捕获的数据传输到 WaveRT 缓冲区并使其可供 OS 读取时设置事件。
6. 请参阅（2）。
对于[**KSNODETYPE \_ audio \_ KEYWORDDETECTOR**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-audio-keyworddetector)关键字检测器引脚，驱动程序应为至少 5000 ms 的音频数据分配足够的内部突发缓冲。 如果在缓冲区溢出之前，操作系统无法在 pin 上创建流，则驱动程序可能会结束内部缓冲活动和可用的关联资源。

## <a name="wake-on-voice"></a>唤醒

唤醒（WoV）使用户能够通过口述特定关键字（例如 "你好 Cortana"），在屏幕上激活和查询语音识别引擎，并使其处于低功耗状态。

此功能允许设备在设备处于低功耗状态时始终倾听用户的声音，包括屏幕关闭和设备处于空闲状态。 它通过使用监听模式来实现此功能，与正常的麦克风录制过程中使用的功率利用率相比，此模式的功耗更低。 低功率语音识别允许用户只需说一个预定义的密钥短语（如 "你好 Cortana"），后跟链式语音短语（如 "我的下一个约会"）来以无人参与的方式调用语音。 无论设备处于使用状态还是空闲状态，都将有效。

音频堆栈负责传达唤醒数据（发言人 ID、关键字触发器、置信度级别），并通知感兴趣的客户端已检测到关键字。

### <a name="validation-on-modern-standby-systems"></a>新式备用系统上的验证

可在[新式备用](https://docs.microsoft.com/windows-hardware/design/device-experiences/modern-standby)系统上使用[针对 AC 电源的新式备用唤醒基本测试](https://docs.microsoft.com/windows-hardware/test/hlk/testref/69df7cf2-6024-4eee-92ee-1506480614ee)来验证来自系统空闲状态的 WoV，并在[HLK](https://docs.microsoft.com/windows-hardware/test/hlk/)中的[DC 电源上检测新式备用唤醒](https://docs.microsoft.com/windows-hardware/test/hlk/testref/614ffb93-eced-45ab-bf7b-e09291a97fd2)基本测试。 这些测试检查系统是否具有硬件关键字 spotter （HW-KWS），是否能够进入最深的运行时空闲平台状态（DRIPS），并且能够从具有小于或等于1秒的系统恢复延迟的新式备用声音命令中唤醒。
