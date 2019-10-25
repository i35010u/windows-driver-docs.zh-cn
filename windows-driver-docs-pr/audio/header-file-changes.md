---
title: 标头文件更改
description: 标头文件更改
ms.assetid: 9212aa8d-bb11-4ade-a70c-274a7ffe83ef
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
- 5.1 环绕声扬声器 WDK 音频
- 环绕声扬声器 WDK 音频
- 标头文件 WDK 音频
- Ksmedia.h
- Dsound
- 通道屏蔽 WDK 音频
- 定位 WDK 音频
- WDM 音频数据格式 WDK
- 数据格式化 WDK 音频，头文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cac6b949cb493e0b71e48c39f64a731aed130bb3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831195"
---
# <a name="header-file-changes"></a>标头文件更改


Windows 驱动程序工具包（WDK）包含两个标头文件，用于定义 Windows 多媒体控制面板支持的扬声器配置：

-   Ksmedia 定义[**KSPROPERTY\_音频\_通道\_config**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-channel-config)属性请求使用的[**KSAUDIO\_通道\_config**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_channel_config)结构的通道掩码。

-   Dsound 定义可提交到**IDirectSound：： SetSpeakerConfig**方法的发言人配置标识符的列表。 有关此方法的详细信息，请参阅 Windows SDK 文档。

在 Windows Server 2003、带有 SP1 的 Windows XP、Windows 2000 和 Windows Me/98 中，Ksmedia 定义了下表中显示的用于5.1 和7.1 通道流的通道掩码。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数名称</th>
<th align="left">通道掩码</th>
<th align="left">扬声器位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSAUDIO_SPEAKER_5POINT1</p></td>
<td align="left"><p>0x3F</p></td>
<td align="left"><p>FL，FR，FC，LFE，BL，BR</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSAUDIO_SPEAKER_7POINT1</p></td>
<td align="left"><p>0xFF</p></td>
<td align="left"><p>FL、FR、FC、LFE、BL、BR、FLC、FRC</p></td>
</tr>
</tbody>
</table>

 

上表中的两个通道掩码代表5.1 发言人配置和7.1 发言人配置。 为了识别相同的两个扬声器配置，Dsound 定义了以下扬声器配置 Id：

```cpp
  #define DSSPEAKER_5POINT1      0x00000006
  #define DSSPEAKER_7POINT1      0x00000007
```

在 Windows XP SP2 及更高版本的 Windows 中，Ksmedia 定义了下表中显示的5.1 和7.1 通道的通道掩码。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数名称</th>
<th align="left">通道掩码</th>
<th align="left">扬声器位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KSAUDIO_SPEAKER_5POINT1</p></td>
<td align="left"><p>0x3F</p></td>
<td align="left"><p>FL，FR，FC，LFE，BL，BR</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSAUDIO_SPEAKER_7POINT1_SURROUND</p></td>
<td align="left"><p>0x63F</p></td>
<td align="left"><p>FL，FR，FC，LFE，BL，BR，SL，SR</p></td>
</tr>
</tbody>
</table>

 

通过比较上述两个表，可以看出以下几点：

-   第一个表中的通道掩码0x3F 的含义未在第二个表中更改，即使在 Windows SP2 和更高版本的 Windows 中，KSAUDIO\_音箱\_5POINT1 被解释为使用 SL 和 SR 扬声器，而不是 BL 和 BR。

-   支持值为0x63F 的新通道掩码。 此通道掩码代表7.1 家庭影院扬声器配置。

-   **注意**   在 windows Vista 和更高版本的 windows 中，不再支持 KSAUDIO\_扬声器\_7POINT1 扬声器配置。 因此，它不是控制面板中的可用选项。

     

为了表示相同的一组扬声器配置，Dsound 定义了以下扬声器配置 Id：

```cpp
  #define DSSPEAKER_5POINT1             0x00000006
  #define DSSPEAKER_7POINT1             0x00000007
  #define DSSPEAKER_7POINT1_SURROUND    0x00000008
  #define DSSPEAKER_7POINT1_WIDE        DSSPEAKER_7POINT1
```

DSSPEAKER\_7POINT1\_环绕在 "控制面板 7.1" 中。 DSSPEAKER\_7POINT1 和 DSSPEAKER\_7POINT1\_宽均为同一7.1 范围配置发言人配置的名称。

有关 DirectSound 的扬声器配置的详细信息，请参阅[DirectSound 发言人-配置设置](directsound-speaker-configuration-settings.md)。

 

 




