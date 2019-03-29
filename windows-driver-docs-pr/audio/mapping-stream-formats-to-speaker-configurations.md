---
title: 将流格式映射到扬声器配置
description: 将流格式映射到扬声器配置
ms.assetid: 6af4a3e3-e24b-449f-84ad-9e8bbc22fdde
keywords:
- 数据格式 WDK 音频
- WDK 音频数据的格式
- WDK 的音频数据格式
- 格式 WDK 音频、 多通道
- 多渠道格式 WDK 音频
- 家庭影院系统 WDK 音频
- 扬声器 WDK 音频、 主页 threater 系统
- 音频驱动程序 WDK、 家庭影院系统
- WDM 音频驱动程序 WDK、 家庭影院系统
- 7.1 家庭影院扬声器 WDK 音频
- 7.1 范围内配置扬声器 WDK 音频
- 范围内的配置扬声器 WDK 音频
- WAVEFORMATEXTENSIBLE
- 录制格式 WDK 音频
- 映射格式
- 系统搅拌机 WDK 音频
- 5.1 环绕音响扬声器 WDK 音频
- 定位 WDK 音频
- WDM 音频数据格式 WDK
- 数据格式以 WDK 音频，映射格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a751f9c44cc38873bf48deac054e6f1bed30824
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563787"
---
# <a name="mapping-stream-formats-to-speaker-configurations"></a>将流格式映射到扬声器配置


当系统询问播放与音频设备的扬声器配置不匹配的流格式，音频驱动程序具有多个选项：

-   拒绝播放流。

-   通过执行一对一映射的各个通道到扬声器播放流。 如果后一个通道已映射到每个演讲者留下任何通道，，丢弃剩余的通道。 相反，如果有任何演讲者未所有后通道的已分配到扬声器，播放通过剩余的扬声器的无声段。

-   播放流通过混合使用的通道在原始流生成精确的所需的扬声器配置的通道数。 如果有更多通道中的原始流比发言人，此方法可避免丢失将导致从放弃过多通道的内容。 可以在软件或硬件中执行混合和格式转换。

有关第三个选项，该驱动程序应避免直接执行软件混合使用。 相反，硬件供应商应安装一个全局效果 (GFX) 软件模块，以先达到的音频设备处理流。 在 Windows Vista 中，全局效果将作为 GFX 音频处理对象 (Apo)。 在 Windows Server 2003 和 Windows XP 中，全局效果已作为 GFX 筛选器实现。 

### <a name="span-idplayinga51channelstreamona71speakerconfigurationspanspan-idplayinga51channelstreamona71speakerconfigurationspanplaying-a-51-channel-stream-on-a-71-speaker-configuration"></a><span id="playing_a_5_1_channel_stream_on_a_7_1_speaker_configuration"></span><span id="PLAYING_A_5_1_CHANNEL_STREAM_ON_A_7_1_SPEAKER_CONFIGURATION"></span>7.1 扬声器配置中播放 5.1 通道 Stream

下图显示了记录 （左） 5.1 环绕音响扬声器配置，但通过 （右） 7.1 家庭影院扬声器配置，将会播放的流。

![说明 7.1 扬声器配置中播放 5.1 流关系图](images/spkrcfg5.png)

在上图中，记录 5.1 格式不包含在 7.1 扬声器配置基准和 b R 扬声器位置的通道信息。 因此，这些两个扬声器是无提示。 （另一个且更加困难的替代方案是为该音频设备能够通过混合使用该录制中的原始六个通道中的内容的基准和 b R 扬声器综合两个额外的通道。）

根据通道掩码位的定义，用于记录显示在上图中左侧的 5.1 流通道掩码应是 0x60F，为以下扬声器位置分配的六个通道：佛罗里达州、 FR、 光纤通道、 LFE，SL 和 sr。 （这是前面所述的端扬声器 5.1 配置）。事实上，5.1 流的通道掩码是 0x3F，而不是 0x60F 的原因，前面所述，现在将进行详细说明。

在早期版本的 Windows (Windows Server 2003，Windows XP with SP1、 Windows 2000 和 Windows Me / 98)，通道掩码 0x3F 的解释取决于它将为以下扬声器位置分配的六个通道在 5.1 格式：佛罗里达州、 FR、 光纤通道、 LFE、 BL 和 b. （这是后演讲者 5.1 配置）。但是，在 Windows Vista、 Windows Server 2003 with SP1 和 Windows XP SP2 中的解释取决于不同： 按照约定，5.1 格式通道掩码 0x3F 解释*侧扬声器*5.1 配置而不是*后演讲者*5.1 配置。

解释这种方式中的通道掩码不需要引入了第二个的 5.1 频道格式说明符来区分从后演讲者 5.1 配置端扬声器 5.1 配置。 这两个配置都非常类似，典型的用户可能很难区分它们。 虽然具有单个 5.1 通道格式说明符可避免让人困惑的用户，但却要求硬件供应商需要记住来解释 0x3F 通道掩码来表示通道 5 和 6，将分配给 SL 和 SR 扬声器位置而不是基准和 b R位置。 作为回报不必记住 5.1 流的通道掩码此特殊用例解释，供应商可以省去用户区分两个非常相似的难点在于 5.1 通道格式说明符。

供应商认为至少某些用户可能想要区分端演讲者 5.1 配置和后扬声器 5.1 配置具有为此目的提供用户界面 (UI) 程序的选项。 通过用户界面，用户可以选择是否 4 和 5 5.1 通道流中的通道应驱动器后演讲者而不是侧面扬声器 7.1 家庭影院扬声器配置中。

### <a name="span-idplayinga71channelstreamona51speakerconfigurationspanspan-idplayinga71channelstreamona51speakerconfigurationspanplaying-a-71-channel-stream-on-a-51-speaker-configuration"></a><span id="playing_a_7_1_channel_stream_on_a_5_1_speaker_configuration"></span><span id="PLAYING_A_7_1_CHANNEL_STREAM_ON_A_5_1_SPEAKER_CONFIGURATION"></span>5.1 扬声器配置中播放 7.1 通道 Stream

下图显示了 7.1 家庭影院扬声器配置 （左） 正在播放通过 （右） 5.1 环绕音响扬声器配置为记录流。 7.1 通道流的通道掩码是 0x63F。

![说明 5.1 扬声器配置中播放 7.1 流关系图](images/spkrcfg6.png)

在此示例中，通道 6 和 7，其中包含端扬声器位置 7.1 配置中的数据，通过端扬声器位置 5.1 配置中播放。 音频设备只需放弃渠道 4 和 5，它在 5.1 配置播放流时包含在 7.1 配置中，后扬声器位置的数据。 正如前面提到，（在上图中未显示） 的另一种方法是，设备能够尝试通过将它们与通道 6 和 7 混合通过 5.1 配置中端扬声器播放它们前保留的渠道 4 和 5 中的内容。

### <a name="span-idsystemmixerbehaviorspanspan-idsystemmixerbehaviorspansystem-mixer-behavior"></a><span id="system_mixer_behavior"></span><span id="SYSTEM_MIXER_BEHAVIOR"></span>系统 Mixer 行为

在 Windows Server 2003、 Windows XP、 Windows 2000 和 Windows Me / 98，通常生成的软件系统混音器 Kmixer.sys 多声道音频设备播放的音频流。 流可以开始之前播放、 系统 mixer 和音频驱动程序必须协商混音器和驱动程序可以处理的流格式。

当系统询问播放一种格式，与音频设备的扬声器配置不匹配的多渠道流，音频驱动程序可以拒绝的请求，案例协商将继续。

系统混音器可以将内容转换从 5.1 通道输入流式传输到 7.1 频道输出流 （对音频设备），反之亦然，尽管它首选若要避免这种转换，以保留输入流的质量。 因此，系统混音器首先会协商询问要接受的最高质量输入流的系统 mixer 与相同的格式的流的驱动程序。 通常情况下，这意味着，是否系统 mixer 具有 5.1 或 7.1 通道格式中的输入的流，它将要求要接受相同格式的流的驱动程序。 如果驱动程序会拒绝此格式，则将继续系统 mixer 协商通过要求驱动程序如果它可以处理其他流格式。

例如，如果 5.1 扬声器配置的音频设备的驱动程序拒绝系统 mixer 为播放 7.1 通道流的请求，系统 mixer 继续协商，7.1 通道流转换为 5.1 通道流的产品/服务。 如果该驱动程序接受这种格式，系统混音器驱动程序的执行流转换。

在设计时音频驱动程序，驱动程序编写器必须决定是否能够处理其自己的格式转换或依赖系统 mixer 来执行转换。 该驱动程序可能需要处理在以下情况下转换：

-   如果驱动程序需要以不同于系统混音器执行转换的方式执行的转换。

-   如果该驱动程序必须播放绕过系统 mixer 的流。

在第二种情况下，如果直接与硬件混合 pin 音频设备上播放从 Microsoft DirectSound 硬件加速缓冲区流可以绕过系统 mixer。 此外，某些"pro 音频"应用程序发送其流直接到音频设备以避免系统 mixer 的延迟，或能够防止混合过程更改原始的音频流中的数字的示例值。

在 Windows Server 2003 SP1 和 Windows XP SP2 中，如果系统 mixer 生成 5.1 频道输出流，mixer 始终设置流的通道掩码为 0x3F。 系统混音器执行此操作，即使它接收通道掩码为 0x60F 5.1 通道输入的流。 此行为，与音频驱动程序永远不会从混音器接收通道掩码为 0x60F 5.1 通道流。

如果系统 mixer 接收通道掩码为 0x63F 7.1 通道输入的流，并生成 （使用通道掩码 0x3F） 5.1 频道输出流，mixer 将通道 6 和 7 中的输入流到 4 和 5 中的输出流的频道。 Mixer 放弃渠道 4 和 5 （适用于两个后置扬声器） 7.1 通道的输入流中。 此行为可确保通过在 5.1 扬声器配置端扬声器播放 7.1 通道流中的两个端扬声器包含内容的通道。

 

 




