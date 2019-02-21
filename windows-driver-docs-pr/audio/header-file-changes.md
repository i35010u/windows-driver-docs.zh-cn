---
title: 标头文件更改
description: 标头文件更改
ms.assetid: 9212aa8d-bb11-4ade-a70c-274a7ffe83ef
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
- 环绕音响扬声器 WDK 音频
- 标头文件 WDK 音频
- Ksmedia.h
- Dsound.h
- 通道掩码 WDK 音频
- 定位 WDK 音频
- WDM 音频数据格式 WDK
- 数据格式以 WDK 音频，标头文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7e27ec98c27599f251f2c49062874110fd43b09
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533025"
---
# <a name="header-file-changes"></a>标头文件更改


Windows Driver Kit (WDK) 包含定义支持的 Windows 多媒体控制面板的演讲者配置的两个标头文件：

-   Ksmedia.h 定义的通道掩码[ **KSAUDIO\_通道\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff537083)结构，它由[ **KSPROPERTY\_音频\_通道\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff537250)属性请求。

-   Dsound.h 定义一组可提交到扬声器配置标识符**IDirectSound::SetSpeakerConfig**方法。 有关此方法的详细信息，请参阅 Windows SDK 文档。

在 Windows Server 2003，Windows XP with SP1、 Windows 2000 和 Windows Me / 98，Ksmedia.h 定义 5.1，7.1 通道流的下表中所示的通道掩码。

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
<td align="left"><p>佛罗里达州、 FR、 FC、 LFE、 BL、 B R</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSAUDIO_SPEAKER_7POINT1</p></td>
<td align="left"><p>0xFF</p></td>
<td align="left"><p>佛罗里达州、 FR、 光纤通道、 LFE、 BL、 BR、 FLC、 FRC</p></td>
</tr>
</tbody>
</table>

 

上表中的两个通道掩码表示 5.1 扬声器配置和 7.1 扬声器配置。 若要标识相同的两个扬声器配置，Dsound.h 定义以下扬声器配置 Id:

```cpp
  #define DSSPEAKER_5POINT1      0x00000006
  #define DSSPEAKER_7POINT1      0x00000007
```

在 Windows XP SP2 和更高版本的 Windows 中，Ksmedia.h 定义通道掩码 5.1，7.1 通道流的表所示。

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
<td align="left"><p>佛罗里达州、 FR、 FC、 LFE、 BL、 B R</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSAUDIO_SPEAKER_7POINT1_SURROUND</p></td>
<td align="left"><p>0x63F</p></td>
<td align="left"><p>佛罗里达州、 FR、 光纤通道、 LFE、 BL、 BR、 SL、 SR</p></td>
</tr>
</tbody>
</table>

 

通过比较两个前面的表，并显示以下几点：

-   第一个表中的通道掩码 0x3F 含义未更改在第二个表中，即使尽管在 Windows SP2 和更高版本的 Windows，KSAUDIO\_演讲者\_5POINT1 解释使用 SL 和 SR 发言人，而不是基准和 b.

-   支持新的通道掩码值 0x63F。 此通道掩码表示 7.1 家庭影院扬声器配置。

-   **请注意**  在 Windows Vista 和更高版本的 Windows，KSAUDIO\_演讲者\_7POINT1 扬声器配置不再受支持。 因此，它不是控制面板中的可用选项。

     

若要表示一组相同的扬声器配置，Dsound.h 定义以下扬声器配置 Id:

```cpp
  #define DSSPEAKER_5POINT1             0x00000006
  #define DSSPEAKER_7POINT1             0x00000007
  #define DSSPEAKER_7POINT1_SURROUND    0x00000008
  #define DSSPEAKER_7POINT1_WIDE        DSSPEAKER_7POINT1
```

DSSPEAKER\_7POINT1\_外侧代码表示在控制面板中的新 7.1 家庭影院扬声器配置。 DSSPEAKER\_7POINT1 和 DSSPEAKER\_7POINT1\_宽都是在同一 7.1 范围内配置扬声器配置名称。

DirectSound 的扬声器配置的详细信息，请参阅[DirectSound 扬声器配置设置](directsound-speaker-configuration-settings.md)。

 

 




