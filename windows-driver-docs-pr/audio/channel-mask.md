---
title: 声道掩码
description: 声道掩码
ms.assetid: 875ed000-ac53-4365-8381-3fe08d45cbcc
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
- LFE 发言人
- 低音 WDK 音频
- 录制格式 WDK 音频
- 播放 WDK 音频
- 通道掩码 WDK 音频
- 掩码位 WDK 音频
- PCM 格式 WDK 音频
- 定位 WDK 音频
- 数据格式以 WDK 音频通道掩码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36c51c3280c8cda55e2bd52fb1979ac053db0f4b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355608"
---
# <a name="channel-mask"></a>声道掩码


在 Windows 中， [ **WAVEFORMATEXTENSIBLE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-waveformatextensible)结构定义多渠道的 PCM 音频流的数据格式。 此结构指定的参数，如示例中的每个 PCM 的位数的流和通道掩码中的通道数。 通道掩码指定的映射到扬声器的通道。 下图显示通道掩码中的单个位。

![说明通道掩码中的单个位的关系图](images/spkrcfg3.png)

通道掩码中的每个位表示特定说话人位置。 如果掩码为特定扬声器位置分配一个通道，表示该位置的掩码位设置为 1;未分配的演讲者职位的所有掩码位将都设置为 0。 WAVEFORMATEXTENSIBLE 结构定义中未显示在上图中，通道掩码附加的位，但这些位正在讨论的家庭影院扬声器配置没有任何关系，并为简单起见，省略了。

编码的通道掩码在上图中的扬声器位置是类似于使用的属性值[ **KSPROPERTY\_音频\_通道\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-channel-config)属性请求。 有关详细信息，请参阅[ **KSAUDIO\_通道\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_channel_config)。

下表显示在上图中的每个掩码位的含义。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">比特数</th>
<th align="left">扬声器位置</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>FL</p></td>
<td align="left"><p>正面左边</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>FR</p></td>
<td align="left"><p>右前</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>FC</p></td>
<td align="left"><p>前端 center</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>LFE</p></td>
<td align="left"><p>低频率效果</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>BL</p></td>
<td align="left"><p>后向左</p></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p>BR</p></td>
<td align="left"><p>右后</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"><p>FLC</p></td>
<td align="left"><p>前端角的中心</p></td>
</tr>
<tr class="even">
<td align="left"><p>7</p></td>
<td align="left"><p>FRC</p></td>
<td align="left"><p>中央右前</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8</p></td>
<td align="left"><p>BC</p></td>
<td align="left"><p>后 center</p></td>
</tr>
<tr class="even">
<td align="left"><p>9</p></td>
<td align="left"><p>SL</p></td>
<td align="left"><p>左侧</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>SR</p></td>
<td align="left"><p>右端</p></td>
</tr>
</tbody>
</table>

 

例如， **7.1 家庭影院扬声器**0x63F，表示流中的八个通道已分配到以下扬声器位置 （和按以下顺序） 通道掩码值描述配置:佛罗里达州、 FR、 FC、 LFE、 BL、 BR、 SL 和 sr。 其他示例，请**7.1 范围内的配置扬声器**配置通道掩码值 0xff，表示流中的八个通道已分配给以下扬声器位置进行了介绍：佛罗里达州、 FR、 FC、 LFE、 BL、 巴西、 FLC 和 FRC。

下图显示了通道掩码 0x63F 之间的对应关系并**7.1 家庭影院扬声器**配置。

![说明 7.1 家庭影院扬声器录制和播放的关系图](images/spkrcfg4.png)

左侧和右侧的上图中显示的音频录制内容读入**7.1 家庭影院扬声器**流格式。 在网格的中心的小圆圈表示该侦听器的位置。 每个小的黑色矩形表示麦克风。 八个通道进行编号从 0 到 7。 FL 麦克风记录到通道 0，FR 麦克风记录到声道 1，依此类推。

上图右侧显示了同一个 7.1 通道流播放通过八个演讲者外侧代码配置。 在这种情况下，每个小的黑色矩形表示演讲者。 七个演讲者将映射到周围侦听器在网格上的位置。 映射不会对 LFE 演讲者 （重低音扩音器）; 分配网格位置此省略基于这些扬声器通常生成仅低频率声音，将无方向的假设。

 

 




