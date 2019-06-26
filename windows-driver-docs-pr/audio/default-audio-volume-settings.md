---
title: 默认的音频音量设置
description: 默认的音频音量设置
ms.assetid: 5d694aa2-5a47-44c5-92d5-ec8c4885820f
keywords:
- 音频适配器 WDK、 音量设置
- 适配器驱动程序 WDK 音频音量设置
- 端口类音频适配器 WDK、 音量设置
- 默认的卷设置
- WDK 的音频的音量设置
- 主音量滑块 WDK 音频
- 卷滑块 WDK 音频
- 声音级别设置 WDK 音频
- 主机卷设置 WDK 音频
- 默认的主机卷设置
- 整卷滑块 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14b908666d2a161af257db02fb87e7023734c02f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359074"
---
# <a name="default-audio-volume-settings"></a>默认的音频音量设置


## <span id="default_audio_volume_settings"></span><span id="DEFAULT_AUDIO_VOLUME_SETTINGS"></span>


SndVol 程序 (请参阅[任务栏和 SndVol32](systray-and-sndvol32.md)) 显示一组的卷滑块。 滑块指示各种音频设备和应用程序，如演讲者和系统声音的音量级别设置。 没有为每个音频输出和输入，一个终结点的卷和每个应用程序的应用程序卷。 音频驱动程序可以仅控制其自己的终结点卷，通过 KSPROPERTY\_音频\_VOLUMELEVEL。 如果该驱动程序不会显式初始化这些卷设置在安装时，操作系统将选择其自己对这些设置的默认值。 选择操作系统的默认值不同时，跨所有 Windows 版本中，和供应商可能需要执行帐户，以确保音量级别设置既不太高，也不太低紧跟其后的驱动程序安装到这些差异。

作为一般规则，如果音频适配器驱动器一组具有自己的物理卷控制的模拟扬声器 INF 文件不应设置默认音量级别过低。 否则，用户可能会尝试通过增加而不是增加声卡上的主卷扬声器的音量补偿。 增强的信号强度弱的结果是降低音频质量。

如果音频适配器没有硬件放大器，请参阅[软件卷控件支持](software-volume-control-support.md)提供软件支持的信息。

**请注意**  如果硬件放大器，则驱动程序设置的范围和默认值通过级别[ **KSPROPERTY\_音频\_VOLUMELEVEL** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-volumelevel)内核流式处理属性。 如果不是硬件放大器，则 Windows 将创建一个软件卷控件 APO。
如果没有物理卷旋钮的发言人可用集合，它应在显示 Windows 为 HID 控件。 这将为卷同样正常向上和向下按钮的键盘; 上的卷Windows 会看到卷旋钮打开，并将卷计划控制相应地 （无论它是一个硬件或软件卷）。

 

理想情况下，如果一套 active 扬声器附带在同一个框中的音频的适配器卡，在工厂应调整卷旋钮演讲者最适用于适配器的默认卷设置的位置上。 如果音频适配器不具有物理卷控件旋钮，请参阅[软件卷控件支持](https://docs.microsoft.com/windows-hardware/drivers/audio/software-volume-control-support)主题，了解有关通过 Windows 提供的软件支持的信息。

**请注意**  如果音频硬件公开硬件卷控件 （如卷旋钮），则驱动程序设置的范围和默认值通过级别[ **KSPROPERTY\_音频\_VOLUMELEVEL** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-volumelevel)内核流式处理的属性。

 

下表显示的卷范围和默认音频的音量级别中的不同版本的 Windows。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows 版本</th>
<th align="left">麦克风默认值</th>
<th align="left">非-麦克风 * 默认值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Windows Vista SP1</td>
<td align="left"><p>默认级别：0.0db</p>
<p>卷范围：-192.0 dB ~ + 12.0dB</p></td>
<td align="left"><p>默认级别：0.0db</p>
<p>卷范围：-192.0 dB ~ 0dB</p></td>
</tr>
<tr class="even">
<td align="left">Windows 7</td>
<td align="left"><p>默认级别: + 30.0dB</p>
<p>卷范围：-192 dB ~ +30.0 dB</p></td>
<td align="left"><p>默认级别：0 dB</p>
<p>卷范围：-192 dB ~ 0 dB</p></td>
</tr>
<tr class="odd">
<td align="left">Windows 8</td>
<td align="left"><p>默认级别：0.0 dB</p>
<p>卷范围：-96 dB ~ + 30 dB</p></td>
<td align="left"><p>默认级别：0.0 dB</p>
<p>卷范围：-96 dB ~ 0 dB</p></td>
</tr>
</tbody>
</table>

 

\*术语非-麦克风描述所有播放设备和非麦克风录音设备。
有关由 Windows 应用程序中的软件卷滑块物理卷滑块的操作特征的信息，请参阅[Audio-Tapered 音量控件](https://docs.microsoft.com/windows/desktop/CoreAudio/audio-tapered-volume-controls)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[自定义默认音频音量设置](customizing-default-audio-volume-settings.md)  



