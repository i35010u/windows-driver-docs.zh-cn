---
title: 将流格式映射到扬声器配置
description: 将流格式映射到扬声器配置
keywords:
- 数据格式化 WDK 音频
- 格式化 WDK 音频、数据
- 音频数据格式 WDK
- 格式化 WDK 音频，多通道
- 多通道格式 WDK 音频
- 家庭影院系统 WDK 音频
- 扬声器 WDK 音频，threater 系统
- 音频驱动程序 WDK，家庭影院系统
- WDM 音频驱动程序 WDK，家庭影院系统
- 7.1 家庭影院扬声器 WDK 音频
- 7.1 宽配置扬声器 WDK 音频
- 宽配置扬声器 WDK 音频
- WAVEFORMATEXTENSIBLE
- 录制格式 WDK 音频
- 映射格式
- 系统 mixers WDK 音频
- 5.1 环绕声扬声器 WDK 音频
- 定位 WDK 音频
- WDM 音频数据格式 WDK
- 数据格式化 WDK 音频，映射格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc4ac00510b9f47d822e785d2f90e7f8ff1d7752
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801039"
---
# <a name="mapping-stream-formats-to-speaker-configurations"></a>将流格式映射到扬声器配置


如果要求播放与音频设备的扬声器配置不匹配的流格式，则音频驱动程序有以下几个选项：

-   拒绝播放流。

-   通过执行单个通道到扬声器的一对一映射来播放流。 如果在通道被映射到每个扬声器之后，会留下任何通道，请丢弃遗留通道。 相反地，如果所有频道都已分配给扬声器，则可以通过遗留的扬声器播放静音。

-   通过混合使用原始流中的通道来精确生成扬声器配置所需的通道数来播放流。 如果原始流中的通道数多于扬声器数，则此方法可避免丢失超出额外通道的内容。 可以在软件或硬件中执行混合转换和格式转换。

对于第三个选项，驱动程序应避免直接执行软件混合。 相反，硬件供应商应该安装 (GFX) 软件模块的全局效果，以便在流到达音频设备之前对其进行处理。 在 Windows Vista 中，全局效果以 GFX 音频处理对象的形式实现 () 。 在 Windows Server 2003 和 Windows XP 中，全局效果作为 GFX 筛选器实现。 

### <a name="span-idplaying_a_5_1_channel_stream_on_a_7_1_speaker_configurationspanspan-idplaying_a_5_1_channel_stream_on_a_7_1_speaker_configurationspanplaying-a-51-channel-stream-on-a-71-speaker-configuration"></a><span id="playing_a_5_1_channel_stream_on_a_7_1_speaker_configuration"></span><span id="PLAYING_A_5_1_CHANNEL_STREAM_ON_A_7_1_SPEAKER_CONFIGURATION"></span>在7.1 扬声器配置上播放5.1 通道流

下图显示了为5.1 环绕声扬声器配置记录的流 (左) ，但通过7.1 家庭影院扬声器配置播放， () 。

![说明如何在7.1 发言人配置上播放5.1 流的示意图](images/spkrcfg5.png)

在上图中，记录的5.1 格式不包含7.1 发言人配置中 BL 和 BR 扬声器位置的通道信息。 因此，这两个扬声器是无提示的。  (另一种方法，这种方法更难用来通过混合录制中的原始六个通道中的内容来为 BL 和 BR 扬声器合成两个附加通道。 ) 

根据通道掩码位的定义，录制上图左侧显示的5.1 流的通道掩码应为0x60F，这会将六个通道分配给以下扬声器位置： FL、FR、FC、LFE、SL 和 SR。  (这是前面讨论过的侧面扬声器5.1 配置。 ) 事实上，5.1 流的通道掩码是0x3F 而不是0x60F，原因是前面提到的原因，现在会详细说明。

在较早版本的 Windows (Windows Server 2003、Windows XP SP1、Windows 2000 和 Windows Me/98) 中，通道掩码0x3F 的解释是将6个通道以5.1 格式分配给以下发言人位置： FL、FR、FC、LFE、BL 和 BR。  (这是后端扬声器5.1 配置。 ) 不过，Windows Vista、Windows Server 2003 SP1 和 Windows XP SP2 中的解释是不同的：按照约定，带有通道掩码0x3F 的5.1 格式将被解释为表示 *侧面发言人* 5.1 配置，而不是 *扬声器* 的5.1 配置。

通过以这种方式解释通道掩码，无需引入另一个5.1 通道格式描述符来区分后扬声器5.1 配置的两侧扬声器5.1 配置。 这两种配置如此相似，典型的用户可能难以区分它们。 尽管只有一个5.1 通道格式描述符可以避免用户混淆，但它确实要求硬件供应商记得解释0x3F 通道掩码，这意味着通道5和6将分配给 SL 和 SR 发言人位置，而不是 BL 和 BR 位置。 为了不必记住这种用于5.1 流的通道掩码的特殊案例解释，供应商可以使用户能够在两个非常相似的5.1 通道格式说明符之间进行区分。

如果供应商认为至少部分用户可能想要区分两侧的扬声器5.1 配置和后扬声器5.1 配置，则可以选择提供用户界面 (UI) 程序来实现此目的。 通过 UI，用户可以选择5.1 声道流中的频道4和5是否应驱动背面的扬声器，而不是7.1 家庭影院扬声器配置中的侧面扬声器。

### <a name="span-idplaying_a_7_1_channel_stream_on_a_5_1_speaker_configurationspanspan-idplaying_a_7_1_channel_stream_on_a_5_1_speaker_configurationspanplaying-a-71-channel-stream-on-a-51-speaker-configuration"></a><span id="playing_a_7_1_channel_stream_on_a_5_1_speaker_configuration"></span><span id="PLAYING_A_7_1_CHANNEL_STREAM_ON_A_5_1_SPEAKER_CONFIGURATION"></span>在5.1 扬声器配置上播放7.1 通道流

下图显示了一个为7.1 家庭影院扬声器配置记录的流， (左侧) 通过5.1 环绕声扬声器配置播放， (右) 。 7.1 通道流的通道掩码为0x63F。

![说明如何在5.1 发言人配置上播放7.1 流的示意图](images/spkrcfg6.png)

在此示例中，通道6和7（其中包含7.1 配置中侧面发言人位置的数据）在5.1 配置中通过侧扬声器位置播放。 音频设备只会丢弃通道4和5，其中包含7.1 配置中后扬声器位置的数据（当它在5.1 配置上播放流时）。 如前所述，上图中未显示的另一种替代方法 () 用于设备尝试在通道4和5中混合内容，然后在5.1 配置中通过侧扬声器将内容与通道6和7混合。

### <a name="span-idsystem_mixer_behaviorspanspan-idsystem_mixer_behaviorspansystem-mixer-behavior"></a><span id="system_mixer_behavior"></span><span id="SYSTEM_MIXER_BEHAVIOR"></span>系统混音器行为

在 Windows Server 2003、Windows XP、Windows 2000 和 Windows Me/98 中，音频设备播放的多通道音频流通常由软件系统混音器（Kmixer.sys）生成。 在流开始播放之前，系统混音器和音频驱动程序必须协商混音器和驱动程序可以处理的流格式。

如果要求使用与音频设备扬声器配置不匹配的格式播放多通道流，则音频驱动程序可以拒绝该请求，在这种情况下，协商将继续。

系统混音器可以将5.1 声道输入流中的内容转换为7.1 通道输出流 (到音频设备) ，反之亦然，尽管它更倾向于避免此类转换来保留输入流的质量。 因此，系统混音器通过请求驱动程序接受与系统混音器的最高质量输入流格式相同的流来开始协商。 通常，这意味着，如果系统混音器具有5.1 或7.1 格式的输入流，它将要求驱动程序接受相同格式的流。 如果驱动程序拒绝此格式，系统混音器会通过询问驱动程序来处理其他流格式，继续协商。

例如，如果具有5.1 扬声器配置的音频设备的驱动程序拒绝系统混音器发出7.1 通道流，系统混音器会继续进行协商，方法是将7.1 通道流转换为5.1 通道流。 如果驱动程序接受此格式，系统混音器将为驱动程序执行流转换。

设计音频驱动程序时，驱动程序编写器必须决定是要处理自己的格式转换还是依赖系统混音器来执行转换。 在以下任一情况下，驱动程序可能需要处理转换：

-   如果驱动程序要求转换的执行方式与系统混音器执行的转换不同。

-   如果驱动程序必须播放绕过系统混音器的流，则为。

在第二种情况下，如果从 Microsoft DirectSound 硬件加速缓冲区直接播放到音频设备上的硬件混合 pin，则流可以绕过系统混音器。 此外，某些 "pro 音频" 应用程序会将其流直接发送到音频设备，以避免系统混音器的延迟，或防止混合过程更改原始音频流中的数字样本值。

在 Windows Server 2003 SP1 和 Windows XP SP2 中，如果系统混音器生成5.1 通道输出流，混音器始终会将流的通道掩码设置为0x3F。 即使系统混音器接收到通道掩码为0x60F 的5.1 通道输入流，系统混音器仍会表现出这种行为。 使用此行为时，音频驱动程序从不从混音器接收通道掩码为0x60F 的5.1 通道流。

如果系统混合器接收到通道掩码为0x63F 的7.1 通道输入流，并生成5.1 通道输出流 (通道掩码为 0x3F) ，则会将输入流中的通道6和7复制到输出流中的通道4和5。 混音器会丢弃7.1 声道输入流中两个后扬声器) 的通道4和 5 (。 此行为可确保通道中的通道包含7.1 通道5.1 流中的两个侧扬声器的内容。

 

 




