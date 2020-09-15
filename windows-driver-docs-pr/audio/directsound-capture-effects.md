---
title: DirectSound 捕获效果
description: DirectSound 捕获效果
ms.assetid: 5dcadcea-0b6a-447d-828d-a7f256f97088
keywords:
- DirectSound WDK 音频，捕获效果
- 回声抵消乐曲音频
- 干扰声音频
- AEC WDK 音频
- 捕获效果 WDK 音频
- 全双工应用程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f62cf595292a9cfb7267d02c73a49412efcdd953
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102366"
---
# <a name="directsound-capture-effects"></a>DirectSound 捕获效果


## <span id="directsound_capture_effects"></span><span id="DIRECTSOUND_CAPTURE_EFFECTS"></span>


DirectSound 8 添加了一些新功能，用于启用和控制音频捕获过程中的第三方效果。 此版本和更高版本的 DirectSound 支持以下两个捕获效果：

-   ) 的声音回声取消 (

-   NS)  (噪音抑制

在全双工音频应用程序（如电话会议）中，将在生成捕获流的麦克风中选取要通过扬声器输出的呈现流的回声。 在房间或其他物理环境中描述声音反射后，全双工系统将使用 AEC 监视呈现流，以取消它添加到捕获流中的回显。 系统可以通过使用 NS 检测噪音峰值，并从流中删除，从而进一步提高捕获流的质量。

全双工 DirectSound 应用程序可以使用 **IDirectSoundCaptureFXAec** 和 **IDirectSoundCaptureFXNoiseSuppress** 接口来控制 AEC 和 NS 的影响。 **IDirectSoundCaptureBuffer：： GetObjectInPath**方法用这些接口检索指向对象的指针。 **DirectSoundFullDuplexCreate**函数将创建**IDirectSoundCaptureBuffer**对象，并且调用方传递给此函数的参数包括一个 DSCEFFECTDESC 结构数组。 数组指定在捕获缓冲区中启用的效果。 数组中每个结构的 **guidDSCFXClass** 成员包含一个指定效果的 GUID： AEC 或 NS。 下表显示了每个 GUID 的 DirectSound 名称，以及同一 GUID 值的 KS 名称。 有关详细信息，请参阅 DirectX 8.0 SDK 文档。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DirectSound GUID 名称</th>
<th align="left">KS GUID 名称</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>GUID_DSCFX_CLASS_AEC</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/audio/ksnodetype-acoustic-echo-cancel" data-raw-source="[&lt;strong&gt;KSNODETYPE_ACOUSTIC_ECHO_CANCEL&lt;/strong&gt;](./ksnodetype-acoustic-echo-cancel.md)"><strong>KSNODETYPE_ACOUSTIC_ECHO_CANCEL</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>GUID_DSCFX_CLASS_NS</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/audio/ksnodetype-noise-suppress" data-raw-source="[&lt;strong&gt;KSNODETYPE_NOISE_SUPPRESS&lt;/strong&gt;](./ksnodetype-noise-suppress.md)"><strong>KSNODETYPE_NOISE_SUPPRESS</strong></a></p></td>
</tr>
</tbody>
</table>

 

在 Microsoft Windows XP 和更高版本中，你可以向 DirectSound 应用程序公开音频设备的硬件加速捕获效果。 此外，AEC 系统筛选器 ( # A0) 提供 AEC 和 NS 影响的软件模拟。

本部分的其余部分讨论了这些主题：

[公开硬件加速捕获效果](exposing-hardware-accelerated-capture-effects.md)

[AEC 系统筛选器](aec-system-filter.md)

