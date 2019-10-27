---
title: 非 PCM 支持的背景
description: 非 PCM 支持的背景
ms.assetid: 4f0e1101-e4cc-4bde-a178-fb47fe24ae4d
keywords:
- 非 PCM 音频格式 WDK，DirectSound
- 非 PCM 音频格式 WDK，waveOut
- waveOut 非 PCM 支持 WDK 音频
- DirectSound WDK 音频，非 PCM 支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69e3060ebb5dd22ae80003d6c9723458f565555f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831275"
---
# <a name="background-of-non-pcm-support"></a>非 PCM 支持的背景


## <span id="background_of_non_pcm_support"></span><span id="BACKGROUND_OF_NON_PCM_SUPPORT"></span>


一些问题阻止了早期版本的 Microsoft Windows 从 waveOut 和 DirectSound Api 支持非 PCM 格式。 下面讨论了这些问题及其解决方法。

### <a name="span-idwaveout_apispanspan-idwaveout_apispanspan-idwaveout_apispanwaveout-api"></a><span id="waveOut_API"></span><span id="waveout_api"></span><span id="WAVEOUT_API"></span>waveOut API

将 waveOut 应用程序与 VxD wave 驱动程序分离的软件层相当薄。 支持自定义波形格式的驱动程序和应用程序可以流式传输该格式的数据，而不管操作系统是否理解格式。

但是，在 Windows 2000 和 Windows 98 中，WDM 音频框架强制由 waveOut API （和 DirectShow 的 waveOut 呈现器）处理的所有音频数据都通过[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)（KMixer），这是内核音频混音器。 仅当 KMixer 支持格式时，waveOutOpen 调用才会成功，而不管驱动程序是否支持该格式。

KMixer 在所有 WDM 操作系统上\_PCM 处理波形\_格式。 Windows 2000 及更高版本和 Windows 98 SE 将 KMixer 扩展为不仅支持波形\_格式\_IEEE\_FLOAT，还支持 PCM 和 IEEE 浮点格式的[**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)变体。 由于 KMixer 不支持任何非 PCM 格式，因此尝试通过 KMixer 传递非 PCM 数据失败。

Windows XP 及更高版本和 Windows Me 通过允许非 PCM 音频数据直接跳过 KMixer，支持非 PCM 格式。 具体而言，waveOut 非 PCM 数据会直接流向 PortCls （或 USBAudio），而不是首先传递到 KMixer。 任何非 PCM 数据的混合都必须在硬件中完成，但使用非 PCM 数据（如 AC-3 或 WMA Pro）的应用程序通常不需要混合和驱动程序通常不支持采用该格式的硬件混合。

### <a name="span-iddirectsound_apispanspan-iddirectsound_apispanspan-iddirectsound_apispandirectsound-api"></a><span id="DirectSound_API"></span><span id="directsound_api"></span><span id="DIRECTSOUND_API"></span>DirectSound API

在传统的 waveOut 驱动程序和 VxD 驱动程序上，DirectSound 支持主和辅助缓冲区的[**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex) （但不是 WAVEFORMATEXTENSIBLE），每个样本有8个或16位，一条或两条通道，以及 100 Hz 和 100 kHz 之间的采样率. 当协作级别设置为 DSSCL\_WRITEPRIMARY 时，VxD 驱动程序可以进一步限制主缓冲区允许使用的格式（请参阅 DirectX SDK 中的**IDirectSoundBuffer：： SetFormat**方法的说明）。 这些限制在 Windows Me 或 Windows XP 中没有更改。

WDM 驱动程序可以支持 WAVEFORMATEX 和 WAVEFORMATEXTENSIBLE 形式的 PCM 格式。 对于 Windows 2000 及更高版本、Windows Me 和 Windows 98 SE，驱动程序还可以支持\_IEEE\_\_格式，同时用于主和辅助 DSBCAPS\_LOCSOFTWARE 缓冲区（由 KMixer 混合）和WAVEFORMATEXTENSIBLE 窗体。

调用**SetFormat**指定主缓冲区的数据格式只对声卡所选的最终混合格式产生间接影响。 主缓冲区对象用于获取**IDirectSound3DListener**接口并设置设备的全局卷和平移，但不表示来自声卡的单个输出流。 相反，KMixer 会混合主缓冲区数据，以允许多个 DSSCL\_WRITEPRIMARY DirectSound 客户端同时运行。

在 Windows 2000 和 Windows 98 上，DirectSound 仅支持 PCM 数据。 （这也是使用 DirectSound 的呈现器的 DirectShow 的情况。）即使驱动程序支持格式，使用非 PCM 格式调用**CreateSoundBuffer**的调用也始终会失败。 出现故障的原因有两个。 首先，无论何时 DirectSound 创建一个 KS pin，都将自动指定 KSDATAFORMAT\_子类型\_PCM，而不是从用于创建该**IDirectSoundBuffer**对象。 其次，DirectSound 要求每个数据路径都有卷和 SRC （采样率转换）节点（[**KSNODETYPE\_卷**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-volume)和[**KSNODETYPE\_src**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-src)），而不考虑客户端请求的是平移、批量还是频率控制DirectSound 缓冲区。 如果数据通过 KMixer 或设备执行硬件混合，则满足此要求。 但对于非 PCM 格式，KMixer 不存在于数据路径中，驱动程序本身通常会在系统要求执行硬件混合时失败。

Windows XP 及更高版本和 Windows Me 消除了阻止 DirectSound 应用程序使用非 PCM 格式的限制。 DirectSound 8 （及更高版本）使用正确的格式子类型，并且不再自动需要每个数据路径中的卷和 SRC 节点。

 

 




