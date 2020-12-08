---
title: 默认的音频音量设置
description: 默认的音频音量设置
keywords:
- 音频适配器 WDK，音量设置
- 适配器驱动程序 WDK 音频，音量设置
- 端口类音频适配器 WDK，音量设置
- 默认卷设置
- 音频音量设置 WDK
- 主音量滑块 WDK 音频
- 音量滑块 WDK 音频
- 声音级别设置 WDK 音频
- 主-卷设置 WDK 音频
- 默认主-批量设置
- 全卷滑块 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 659531730de01de539e2fedf37a8ed581853ff63
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789303"
---
# <a name="default-audio-volume-settings"></a>默认的音频音量设置


## <span id="default_audio_volume_settings"></span><span id="DEFAULT_AUDIO_VOLUME_SETTINGS"></span>


SndVol 程序 (参阅 " [托盘和 SndVol32](systray-and-sndvol32.md) ") 显示一组音量滑杆。 滑块指示各种音频设备和应用程序（如扬声器和系统声音）的卷级别设置。 每个音频输出和输入都有一个终结点卷，每个应用程序都有一个应用程序卷。 音频驱动程序通过 KSPROPERTY 音频 VOLUMELEVEL 仅控制其自己的终结点 \_ 卷 \_ 。 如果驱动程序在安装时未显式初始化这些卷设置，操作系统将为这些设置选择自己的默认值。 操作系统选择的默认值在所有 Windows 版本中都不相同，并且供应商可能需要考虑到这些差异，以确保在安装驱动程序后，卷级别的设置既不太高，也不会过低。

一般规则是，如果音频适配器驱动一组具有其自己的物理音量控制的模拟扬声器，则 INF 文件不应将默认音量级别设置得过低。 否则，用户可能会尝试通过提高扬声器的音量而不是在声卡上增加主音量来进行补偿。 低信号级别的放大的结果是音频质量的损失。

如果音频适配器没有硬件放大器，请参阅 [软件音量控制支持](software-volume-control-support.md) ，了解有关提供的软件支持的信息。

**注意**  如果有硬件放大器，则驱动程序将通过 [**KSPROPERTY \_ 音频 \_ VOLUMELEVEL**](./ksproperty-audio-volumelevel.md) 内核流式处理属性设置范围和默认级别。 如果没有硬件放大器，Windows 将创建软件音量控制 APO。
如果活动的扬声器集上有一个物理卷旋钮，则它应作为 HID 控件出现在 Windows 中。 此功能类似于键盘上的 "音量调出" 和 "音量减小" 按钮;Windows 将看到卷旋钮轮变成，并将相应地对音量控制进行编程 (不管是硬件还是软件卷。 ) 

 

理想情况下，如果一组活动扬声器随附在音频适配器卡的同一个框中，则工厂应将扬声器的音量旋钮调整到最适合使用适配器的默认音量设置的位置。 如果音频适配器没有物理音量控制旋钮，请参阅 [软件音量控制支持](./software-volume-control-support.md) 主题，了解有关 Windows 提供的软件支持的信息。

**注意**  如果音频硬件 (如卷旋钮) 中显示硬件卷控制，则驱动程序将通过 [**KSPROPERTY \_ audio \_ VOLUMELEVEL**](./ksproperty-audio-volumelevel.md) 内核流式处理属性设置范围和默认级别。

 

下表显示了不同版本的 Windows 中音频的卷范围和默认卷级别。

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
<th align="left">非麦克风 * 默认值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Windows Vista SP1</td>
<td align="left"><p>默认级别： 0.0 db</p>
<p>卷范围：-192.0 dB ~ + 12.0 dB</p></td>
<td align="left"><p>默认级别： 0.0 db</p>
<p>卷范围：-192.0 dB ~ 0dB</p></td>
</tr>
<tr class="even">
<td align="left">Windows 7</td>
<td align="left"><p>默认级别： + 30.0 dB</p>
<p>卷范围：-192 dB ~ + 30.0 dB</p></td>
<td align="left"><p>默认级别： 0 dB</p>
<p>卷范围：-192 dB ~ 0 dB</p></td>
</tr>
<tr class="odd">
<td align="left">Windows 8</td>
<td align="left"><p>默认级别： 0.0 dB</p>
<p>卷范围：-96 dB ~ + 30 dB</p></td>
<td align="left"><p>默认级别： 0.0 dB</p>
<p>卷范围：-96 dB ~ 0 dB</p></td>
</tr>
</tbody>
</table>

 

\*非麦克风这一术语描述了所有播放设备和录制设备而不是麦克风。
有关 Windows 应用程序中的 "软件音量" 滑块所表示的物理音量滑杆的操作特征的信息，请参阅 " [音频-锥形音量控制](/windows/desktop/CoreAudio/audio-tapered-volume-controls)"。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[自定义默认音频音量设置](customizing-default-audio-volume-settings.md)
