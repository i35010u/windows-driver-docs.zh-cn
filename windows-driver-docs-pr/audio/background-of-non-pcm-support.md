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
ms.openlocfilehash: 3d01020d43006d09bc5437d752eef518e114630b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208241"
---
# <a name="background-of-non-pcm-support"></a>非 PCM 支持的背景


## <span id="background_of_non_pcm_support"></span><span id="BACKGROUND_OF_NON_PCM_SUPPORT"></span>


一些问题阻止了早期版本的 Microsoft Windows 从 waveOut 和 DirectSound Api 支持非 PCM 格式。 下面讨论了这些问题及其解决方法。

### <a name="span-idwaveout_apispanspan-idwaveout_apispanspan-idwaveout_apispanwaveout-api"></a><span id="waveOut_API"></span><span id="waveout_api"></span><span id="WAVEOUT_API"></span>waveOut API

将 waveOut 应用程序与 VxD wave 驱动程序分离的软件层相当薄。 支持自定义波形格式的驱动程序和应用程序可以流式传输该格式的数据，而不管操作系统是否理解格式。

但是，在 Windows 2000 和 Windows 98 中，WDM 音频框架会强制由 waveOut API 处理的所有音频数据 (，而 DirectShow 的 waveOut) 呈现器将通过 [KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver) ( # A0) ，这是内核音频混音器。 仅当 KMixer 支持格式时，waveOutOpen 调用才会成功，而不管驱动程序是否支持该格式。

KMixer 处理 \_ \_ 所有 WDM 操作系统上的波形格式 PCM。 Windows 2000 及更高版本和 Windows 98 SE 将 KMixer 扩展为不仅支持波形 \_ 格式 \_ IEEE \_ FLOAT，还支持 PCM 和 IEEE-FLOAT 格式的 [**WAVEFORMATEXTENSIBLE**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible) 变体。 由于 KMixer 不支持任何非 PCM 格式，因此尝试通过 KMixer 传递非 PCM 数据失败。

Windows XP 及更高版本和 Windows Me 通过允许非 PCM 音频数据直接跳过 KMixer，支持非 PCM 格式。 具体而言，waveOut 非 PCM 数据会直接流向 PortCls (或 USBAudio) ，而不是首先传递 KMixer。 任何非 PCM 数据的混合都必须在硬件中完成，但使用非 PCM 数据（如 AC-3 或 WMA Pro）的应用程序通常不需要混合和驱动程序通常不支持采用该格式的硬件混合。

### <a name="span-iddirectsound_apispanspan-iddirectsound_apispanspan-iddirectsound_apispandirectsound-api"></a><span id="DirectSound_API"></span><span id="directsound_api"></span><span id="DIRECTSOUND_API"></span>DirectSound API

在传统的 waveOut 驱动程序和 VxD 驱动程序上，DirectSound 支持 [**WAVEFORMATEX**](/windows/desktop/api/mmreg/ns-mmreg-twaveformatex) (但不能) PCM 格式用于主和辅助缓冲区，每个样本有8个或16位、一个或两个通道，以及 100 Hz 到 100 kHz 之间的采样速率。 当协作级别设置为 DSSCL WRITEPRIMARY 时，VxD 驱动程序可以进一步限制主缓冲区允许的格式 \_ (参阅 DIRECTX SDK 中的 **IDirectSoundBuffer：： SetFormat** 方法的说明) 。 这些限制在 Windows Me 或 Windows XP 中没有更改。

WDM 驱动程序可以支持 WAVEFORMATEX 和 WAVEFORMATEXTENSIBLE 形式的 PCM 格式。 对于 Windows 2000 及更高版本、Windows Me 和 Windows 98 SE，驱动程序还可以支持 \_ \_ \_ \_ LOCSOFTWARE 和 WAVEFORMATEXTENSIBLE 形式 () 混合的主和辅助 DSBCAPS 缓冲区的波形格式 IEEE 浮点格式。

调用 **SetFormat** 指定主缓冲区的数据格式只对声卡所选的最终混合格式产生间接影响。 主缓冲区对象用于获取 **IDirectSound3DListener** 接口并设置设备的全局卷和平移，但不表示来自声卡的单个输出流。 相反，KMixer 会混合主缓冲区数据，以允许多个 DSSCL \_ WRITEPRIMARY DirectSound 客户端同时运行。

在 Windows 2000 和 Windows 98 上，DirectSound 仅支持 PCM 数据。  (这种情况同样适用于 DirectShow，这种情况下会使用 DirectSound 的呈现器。 ) 使用非 PCM 格式对 **CreateSoundBuffer** 的调用始终会失败，即使驱动程序支持格式也是如此。 出现故障的原因有两个。 首先，每当 DirectSound 创建一个 KS pin 时，它都会自动指定 KSDATAFORMAT \_ 子类型 \_ PCM，而不是从用于创建**IDIRECTSOUNDBUFFER**对象的 WAVEFORMATEX 结构的**wFormatTag**成员派生子类型。 其次，DirectSound 要求每个数据路径都具有卷和 SRC (采样速率转换) 节点 ([**KSNODETYPE \_ 卷**](./ksnodetype-volume.md) 和 [**KSNODETYPE \_ SRC**](./ksnodetype-src.md)) ，而不考虑客户端请求 DirectSound 缓冲区上的平移、音量还是频率控制。 如果数据通过 KMixer 或设备执行硬件混合，则满足此要求。 但对于非 PCM 格式，KMixer 不存在于数据路径中，驱动程序本身通常会在系统要求执行硬件混合时失败。

Windows XP 及更高版本和 Windows Me 消除了阻止 DirectSound 应用程序使用非 PCM 格式的限制。 DirectSound 8 (及更高版本) 使用正确的格式子类型，并且不再自动需要每个数据路径中的卷和 SRC 节点。

 

