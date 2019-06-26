---
title: 非 PCM 支持的背景
description: 非 PCM 支持的背景
ms.assetid: 4f0e1101-e4cc-4bde-a178-fb47fe24ae4d
keywords:
- 非 PCM 音频格式 WDK DirectSound
- 非 PCM 音频格式 WDK，waveOut
- waveOut 非 PCM 支持 WDK 音频
- DirectSound WDK 音频，非 PCM 支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2565f18319074ecbb91f689931bcf6e4f899ab0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356536"
---
# <a name="background-of-non-pcm-support"></a>非 PCM 支持的背景


## <span id="background_of_non_pcm_support"></span><span id="BACKGROUND_OF_NON_PCM_SUPPORT"></span>


几个问题阻止 Microsoft Windows 的早期版本支持通过 waveOut 和 DirectSound Api 非 PCM 格式。 下面讨论了这些问题和如何它们已得到了解决。

### <a name="span-idwaveoutapispanspan-idwaveoutapispanspan-idwaveoutapispanwaveout-api"></a><span id="waveOut_API"></span><span id="waveout_api"></span><span id="WAVEOUT_API"></span>waveOut API

用于分隔 waveOut VxD 批驱动程序的应用程序的软件层是相当薄。 驱动程序和支持自定义声波格式的应用程序可以将流中的格式而不考虑操作系统是否理解的格式的数据。

但是，在 Windows 2000 和 Windows 98，WDM 音频 framework 强制所有由 waveOut API （和 DirectShow 的 waveOut 呈现器） 来传递处理的音频数据[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)(Kmixer.sys)，即音频混音器内核。 仅当 KMixer 支持的格式，而不考虑该驱动程序是否支持的格式，waveOutOpen 调用会成功。

KMixer 处理批\_格式\_所有 WDM 操作系统上的 PCM。 Windows 2000 和更高版本、 和 Windows 98 SE 扩展 KMixer 以支持不仅 WAVE\_格式\_IEEE\_FLOAT 还[ **WAVEFORMATEXTENSIBLE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-waveformatextensible)的变体PCM 和 IEEE 浮点格式。 由于 KMixer 不支持任何非 PCM 格式，因此尝试将非 PCM 数据通过 KMixer 传递将失败。

Windows XP 及更高版本，和 Windows Me 中，通过允许非 PCM 音频数据，只需跳过 KMixer 支持非 PCM 格式。 具体而言，waveOut 非 PCM 数据直接向 PortCls （或 USBAudio） 而不是通过 KMixer 的第一个传入流。 混合使用任何非 PCM 数据必须完成中的硬件，但应用程序中的格式如 ac-3 或 WMA Pro 使用非 PCM 数据通常不需要混合和驱动程序通常不支持该格式中混合使用的硬件。

### <a name="span-iddirectsoundapispanspan-iddirectsoundapispanspan-iddirectsoundapispandirectsound-api"></a><span id="DirectSound_API"></span><span id="directsound_api"></span><span id="DIRECTSOUND_API"></span>DirectSound API

旧 waveOut 驱动程序和 VxD 驱动程序，支持 DirectSound [ **WAVEFORMATEX** ](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex) （但不是 WAVEFORMATEXTENSIBLE） 的主要和次要缓冲区，每个样本，8 或 16 位的 PCM 格式之一或两个通道，并介于 100 Hz，100 kHz 之间的采样速率。 VxD 驱动程序可能会进一步限制时的协作性级别设置为 DSSCL 允许使用的主缓冲区的格式\_WRITEPRIMARY (请参阅的说明**IDirectSoundBuffer::SetFormat** DirectX SDK 中的方法)。 在 Windows Me 或 Windows XP 中未更改这些限制。

WDM 驱动程序可以支持 WAVEFORMATEX 和 WAVEFORMATEXTENSIBLE 窗体中的 PCM 格式。 Windows 2000 和更高版本，Windows Me 和 Windows 98 SE 中，驱动程序还可以支持批\_格式\_IEEE\_浮点格式的主要和次要 DSBCAPS\_LOCSOFTWARE 缓冲区 （通过 KMixer 混合） 中WAVEFORMATEX 和 WAVEFORMATEXTENSIBLE 窗体。

调用**SetFormat**以指定的数据的主缓冲区格式具有仅间接影响最终混合格式选择的声卡的步骤。 主缓冲区对象用于获取**IDirectSound3DListener**接口，并设置设备的全局音量和平移，但不的表示单个输出流从声卡的步骤。 相反，KMixer 混合的主缓冲区数据使用以允许多个 DSSCL\_WRITEPRIMARY DirectSound 客户端同时运行。

在 Windows 2000 和 Windows 98，DirectSound 仅支持 PCM 数据。 （这同样适用的 DirectShow，使用 DirectSound 的呈现器。）调用**CreateSoundBuffer**与非 PCM 格式始终会失败，即使该驱动程序支持的格式。 出现故障，原因有两个。 首先，每当 DirectSound 创建 KS pin，它会自动指定了 KSDATAFORMAT\_子类型\_而不是派生的子类型从 PCM **wFormatTag**是 WAVEFORMATEX 结构中的成员用于创建**IDirectSoundBuffer**对象。 其次，DirectSound 需要每个数据路径具有卷和 SRC （采样率转换） 节点 ([**KSNODETYPE\_卷**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume)并[ **KSNODETYPE\_SRC**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-src))，无论是否在客户端请求平移、 卷或频率 DirectSound 缓冲区上的控件。 如果数据通过 KMixer 或设备执行硬件混合使用可满足此要求。 对于非 PCM 格式，但是，KMixer 中不存在的数据路径，并且要求执行硬件混合时，通常会失败的驱动程序本身。

Windows XP 及更高版本，和 Windows Me 中，删除使 DirectSound 应用程序无法使用非 PCM 格式的限制。 DirectSound 8 （和更高版本） 使用正确的格式的子类型，并不再自动要求卷和每个数据路径中的 SRC 节点。

 

 




