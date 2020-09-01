---
title: 声道掩码
description: 声道掩码
ms.assetid: 875ed000-ac53-4365-8381-3fe08d45cbcc
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
- LFE 扬声器
- subwoofers WDK 音频
- 录制格式 WDK 音频
- 播放 WDK 音频
- 通道屏蔽 WDK 音频
- 掩码位 WDK 音频
- PCM 音频格式
- 定位 WDK 音频
- 数据格式化 WDK 音频，通道掩码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29741fae5632cbd3d26657778f886f2c1cd3a705
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208221"
---
# <a name="channel-mask"></a>声道掩码


在 Windows 中， [**WAVEFORMATEXTENSIBLE**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible) 结构定义多通道 PCM 音频流的数据格式。 此结构指定参数，例如每个 PCM 样本的位数、流中的通道数和通道掩码。 通道掩码指定到扬声器的通道映射。 下图显示通道掩码中的单个位。

![阐释通道掩码中各个位的关系图](images/spkrcfg3.png)

通道掩码中的每个位代表一个特定发言人位置。 如果掩码向特定发言人位置分配通道，则表示该位置的掩码位设置为 1;未分配的发言人位置的所有掩码位均设置为0。 WAVEFORMATEXTENSIBLE 结构在通道掩码中定义了上图中未显示的其他位，但是，这些位不会与讨论下的家庭影院扬声器配置有关，因此它们会被忽略。

上图中的通道掩码中扬声器位置的编码类似于用于 [**KSPROPERTY \_ 音频 \_ 通道 \_ 配置**](./ksproperty-audio-channel-config.md) 属性请求的属性值的编码。 有关详细信息，请参阅 [**KSAUDIO \_ 信道 \_ CONFIG**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_channel_config)。

下表显示了上图中每个掩码位的含义。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">位数</th>
<th align="left">发言人位置</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>FL</p></td>
<td align="left"><p>左前方</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>FR</p></td>
<td align="left"><p>右前方</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>FC</p></td>
<td align="left"><p>前端中心</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>LFE</p></td>
<td align="left"><p>低频率效果</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>BL</p></td>
<td align="left"><p>左移</p></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p>BR</p></td>
<td align="left"><p>向右</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"><p>FLC</p></td>
<td align="left"><p>居中左前方</p></td>
</tr>
<tr class="even">
<td align="left"><p>7</p></td>
<td align="left"><p>FRC</p></td>
<td align="left"><p>居中右前方</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8</p></td>
<td align="left"><p>BC</p></td>
<td align="left"><p>后中心</p></td>
</tr>
<tr class="even">
<td align="left"><p>9</p></td>
<td align="left"><p>SL</p></td>
<td align="left"><p>左边缘</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>SR</p></td>
<td align="left"><p>右边缘</p></td>
</tr>
</tbody>
</table>

 

例如， **7.1 家庭影院扬声器** 的配置通过 "0x63F" 的通道掩码值进行描述，这表示将流中的8个通道分配给以下扬声器位置， (和顺序如下) ： FL，FR，FC，LFE，BL，BR，SL，和 SR。 另一个示例是， **7.1 范围的配置扬声器** 配置由通道掩码值0xff 描述，这表示将流中的八个通道分配给以下发言人位置： FL、FR、FC、LFE、BL、BR、FLC 和 FRC。

下图显示通道掩码0x63F 和 **7.1 家庭影院扬声器** 配置之间的对应关系。

![说明7.1 家庭影院扬声器录制和播放的示意图](images/spkrcfg4.png)

上图的左侧显示音频内容到 **7.1 家庭影院扬声器** 流格式的录制。 网格中心的小圆圈表示侦听器的位置。 每个小的黑色矩形表示一个麦克风。 8个通道的编号为0到7。 FL 麦克风记录到通道0中，将 FR 麦克风记录到通道1，依此类推。

上图的右侧显示了使用8个扬声器环绕配置播放的同一7.1 通道流。 在这种情况下，每个小型黑色矩形表示一个扬声器。 7个扬声器映射到侦听器周围网格上的位置。 该映射不会 (低音炮) 将网格位置分配给 LFE 扬声器;这种说法的假设是，这些扬声器通常仅生成低频率声音，这是 nondirectional 的。

 

