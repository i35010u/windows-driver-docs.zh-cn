---
title: DirectSound 捕获效果
description: DirectSound 捕获效果
ms.assetid: 5dcadcea-0b6a-447d-828d-a7f256f97088
keywords:
- DirectSound WDK 音频捕获效果
- 回声取消 WDK 音频
- 干扰抑制 WDK 音频
- AEC WDK 音频
- 捕获效果 WDK 音频
- 全双工应用程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 360bf96203c3b8b0b22b2a33de02262421479d28
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543395"
---
# <a name="directsound-capture-effects"></a>DirectSound 捕获效果


## <span id="directsound_capture_effects"></span><span id="DIRECTSOUND_CAPTURE_EFFECTS"></span>


DirectSound 8 添加了用于启用和控制音频捕获过程的第三方效果一些新功能。 这和更高版本的 DirectSound 支持以下两个捕获影响：

-   回声抵消 (AEC)

-   干扰抑制 (NS)

在全双工音频应用程序如电话会议，回显正通过演讲者的输出的呈现器流中提取的麦克风，会生成捕获流。 描述特性中的空间或其他物理环境声音的反射之后, 全双工系统使用 AEC 来监视呈现流来抵消此函数添加到捕获流回显。 通过使用 NS 检测干扰峰值和从流中删除，系统可以进一步提高捕获流的质量。

全双工 DirectSound 应用程序可以使用**IDirectSoundCaptureFXAec**并**IDirectSoundCaptureFXNoiseSuppress**接口来控制 AEC 和 NS 效果。 **IDirectSoundCaptureBuffer::GetObjectInPath**方法检索指向与这些接口的对象的指针。 **DirectSoundFullDuplexCreate**函数创建**IDirectSoundCaptureBuffer**对象，并在调用方传递给此函数的参数包括 DSCEFFECTDESC 结构的数组。 该数组指定要启用捕获缓冲区中的效果。 **GuidDSCFXClass**数组中每个结构成员包含指定有效的 GUID:AEC 或 NS。 每个 GUID DirectSound 名称下的表，以及相同的 GUID 值 KS 名称所示。 有关详细信息，请参阅 DirectX 8.0 SDK 文档。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537150" data-raw-source="[&lt;strong&gt;KSNODETYPE_ACOUSTIC_ECHO_CANCEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537150)"><strong>KSNODETYPE_ACOUSTIC_ECHO_CANCEL</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>GUID_DSCFX_CLASS_NS</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537182" data-raw-source="[&lt;strong&gt;KSNODETYPE_NOISE_SUPPRESS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537182)"><strong>KSNODETYPE_NOISE_SUPPRESS</strong></a></p></td>
</tr>
</tbody>
</table>

 

在 Microsoft Windows XP 及更高版本，可以公开到 DirectSound 应用程序的音频设备的硬件加速捕获效果。 此外，AEC 系统筛选器 (Aec.sys) 提供 AEC 和 NS 效果的软件的模拟。

在本部分的其余部分讨论了这些主题：

[公开硬件加速捕获效果](exposing-hardware-accelerated-capture-effects.md)

[AEC 系统筛选器](aec-system-filter.md)

 

 




