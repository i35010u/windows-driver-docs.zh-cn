---
title: 适用于家庭影院系统的多声道格式
description: 适用于家庭影院系统的多声道格式
ms.assetid: b8bd1dc7-c9a8-4f4f-8014-d31f1ae5361a
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
- 5.1 环绕音响扬声器 WDK 音频
- 环绕音响扬声器
- Sony 动态数字声音
- SDD 配置 WDK 音频
- 流格式 WDK 音频、 多通道
- 定位 WDK 音频
- WDM 音频数据格式 WDK
- 数据格式以 WDK 音频、 多渠道
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e668d94b8a288e2bf960ef4333033370e4c0a25
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332320"
---
# <a name="multichannel-formats-for-home-theater-systems"></a>适用于家庭影院系统的多声道格式


用于家庭影院系统的成本相对较低的解决方案是连接到运行 Windows 操作系统的计算机上的音频适配器的一套环绕声扬声器。 或者，用户可以连接外部音频/视频 (A / V) 适配器输出和演讲者之间的接收方。 家庭影院系统的受欢迎程度响应，5.1 和 7.1 渠道进行创作为这些系统的音频内容变得越来越多地可用。

若要准确地呈现多渠道的家庭影院系统上的音频内容需要可以将扬声器位置分配给多通道流中的音频声道的音频格式描述符。 如前所述， [ **WAVEFORMATEXTENSIBLE** ](https://msdn.microsoft.com/library/windows/hardware/ff538802)结构可以指定此类演讲者分配。

为了帮助为家庭影院系统提供的音频驱动程序支持，Microsoft 还定义了新的 7.1 通道扬声器配置 Microsoft Windows XP 及更高版本。 在 Windows Vista 中，Windows XP Service Pack 2 (SP2) 和 Windows Server 2003 Service Pack 1 (SP1) 支持此配置。 它不支持在 Windows Server 2003 中未安装 service pack，带 Service Pack 1 的 Windows XP 或 Windows XP 安装任何 service pack。

新的 7.1 通道扬声器配置所示下图中，它摘录中 Windows XP SP2 的 Windows 多媒体控件面板 (Mmsys.cpl)。

![新的 7.1 通道扬声器配置图 ](images/spkrcfg1new.gif)

Windows 多媒体控制面板将名称"7.1 家庭影院扬声器"分配给在上图中所示的新 7.1 通道宽扬声器配置。

下图显示了较旧的 7.1 通道配置，这是 Windows 2000 及更高版本和支持 Windows 我 / 98。

![较旧的 7.1 通道宽配置图](images/spkrcfg1old.gif)

在 Windows XP sp2 中，多媒体控制面板将名称"7.1 范围内的配置扬声器"分配给在上图中所示的较旧配置。

在 Windows XP sp2 中，您可以找到通过执行以下步骤在两个以上各图所示的两个配置：

1.  在 Control Panel （类别视图） 中，单击**声音、 语音和音频设备**。

2.  在中**声音、 语音和音频设备**窗格下**挑选一项任务**，单击**调整系统卷**。

3.  在中**声音和音频设备属性**属性工作表，在**卷**选项卡上，在**扬声器设置**，单击**高级**。

4.  在中**高级音频属性**属性工作表，在**扬声器设置**，打开下拉列表并选择一种两个 7.1 演讲者配置。

7.1 宽配置扬声器图中所示的配置是 Sony 动态数字声音 (SDD) 的配置，在用于动画影院 1993年中引入。 但是，如果有，几家庭影院系统使用此配置。 相反，8 扬声器家庭影院系统都可能会使用新的 7.1 配置 7.1 家庭影院扬声器图中所示。 此外，对于 SDD 配置中，是编写的最小的家庭影院内容和用户可以期望的大部分可用的 7.1 通道内容，为新的 7.1 配置要设置格式。

尽管新的"7.1 家庭影院扬声器"配置很大程度上取代旧的"7.1 范围内的配置扬声器"配置，Windows 将继续支持旧配置，以提供向后兼容性。

在 Windows 2000 及更高版本和 Windows Me / 98，5.1 通道扬声器配置向通道 5 和 6 后左和后右扬声器分别。 在 Windows Vista、 Windows Server 2003 with SP1 和 Windows XP SP2，5.1 通道配置保持不变。 7.1 通道配置与这些 Windows 版本不定义新的 5.1 格式说明符来区分从 5.1 后扬声器配置 5.1 端扬声器配置。 由于两个配置都非常类似，定义两个 5.1 配置可能会导致在要使用哪个配置相关用户之间的混淆和是否播放内容编写的其他配置上的多配置。 当定位演讲者 6 演讲者家庭影院系统中，用户往往不区分端和后扬声器位置。 相反，定位的演讲者是更有可能由聊天室的形状和家具房间内的位置。

5.1 通道环绕声扬声器配置所示下图中，它摘录中 Windows XP SP2 的 Windows 多媒体控件面板。

![5.1 通道环绕声扬声器配置图 ](images/spkrcfg2.gif)

Windows 多媒体控制面板将分配名称"5.1 环绕音响扬声器"5.1 通道扬声器配置为在上图中所示。

尽管 5.1 通道端演讲者和后扬声器配置之间的差异可能会对用户透明的但它们不是透明的音频硬件供应商。 正如前面提到，5.1 通道通常创建的内容都端扬声器而不是后置扬声器。 因此，在播放 5.1 通道通过"7.1 家庭影院扬声器"配置的内容，供应商应确保通过端演讲者而不是后置扬声器播放 5.1 通道流中的两个端演讲者通道。 同样，当播放内容时通过端者 5.1 扬声器配置的"7.1 家庭影院扬声器"配置其创作，7.1 端演讲者的通道都将最自然映射到端演讲者 5.1 配置中。 对于音频设备使用流处理功能，另一种方法是，设备能够尝试通过将它们与通道 6 和 7 混合通过 5.1 配置中端扬声器播放它们前保留的渠道 4 和 5 中的内容。

本部分包括：

[通道掩码](channel-mask.md)

[映射到扬声器配置 Stream 格式](mapping-stream-formats-to-speaker-configurations.md)

[标头文件更改](header-file-changes.md)

 

 




