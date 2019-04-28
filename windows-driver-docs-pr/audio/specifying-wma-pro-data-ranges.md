---
title: 指定 WMA Pro 数据范围
description: 指定 WMA Pro 数据范围
ms.assetid: c7e9bc68-cec2-4a34-9ef0-ce3c9a4cc987
keywords:
- S/PDIF 传递 WDK 音频
- WMA Pro-反复-S/PDIF 格式 WDK 音频
- 音频非 PCM 格式 WDK
- 非 PCM 音频格式 WDK、 S/PDIF
- WMA Pro WDK 音频
- 索尼/菲利普数字接口
- 数据范围 WDK 音频、 WMA Pro
- 非 PCM 的音频格式 WDK、 WMA Pro
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 757c87ccc2234773b6570bde8b4a0e5f56cc0ffe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328617"
---
# <a name="specifying-wma-pro-data-ranges"></a>指定 WMA Pro 数据范围


## <span id="specifying_wma_pro_data_ranges"></span><span id="SPECIFYING_WMA_PRO_DATA_RANGES"></span>


标头文件 Mmreg.h 定义值 0x0164 为 WMA Pro-反复-S/PDIF 波形格式标记：

```cpp
  #define WAVE_FORMAT_WMASPDIF  0x0164
```

可以通过使用定义方面波形格式标记指定相应的子类型格式的 GUID\_WAVEFORMATEX\_标头中的 GUID 宏文件 Ksmedia.h，如下所示：

```cpp
  #define KSDATAFORMAT_SUBTYPE_WMA_SPDIF    \
                      DEFINE_WAVEFORMATEX_GUID(WAVE_FORMAT_WMASPDIF)
```

以下代码示例演示如何指定 WaveCyclic 或 WavePci 微型端口驱动程序[ **KSDATARANGE\_音频**](https://msdn.microsoft.com/library/windows/hardware/ff537096)表支持 WMA Pro-反复-S/PDIF pin 条目和AC-3-over-S/PDIF 格式：

```cpp
static KSDATARANGE_AUDIO PinDataRangesSpdifOut[] =
{
  // 48-kHz WMA Pro over S/PDIF
  {
    {
      sizeof(KSDATARANGE_AUDIO),
      0,
      0,
      0,
      STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO),
      STATICGUIDOF(KSDATAFORMAT_SUBTYPE_WMA_SPDIF),
      STATICGUIDOF(KSDATAFORMAT_SPECIFIER_WAVEFORMATEX)
    },
    2,       // Max number of channels
    16,      // Minimum number of bits per sample
    16,      // Maximum number of bits per channel
    48000,   // Minimum rate
    48000    // Maximum rate
  },

  // 44.1-kHz WMA Pro over S/PDIF
  {
    {
      sizeof(KSDATARANGE_AUDIO),
      0,
      0,
      0,
      STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO),
      STATICGUIDOF(KSDATAFORMAT_SUBTYPE_WMA_SPDIF),
      STATICGUIDOF(KSDATAFORMAT_SPECIFIER_WAVEFORMATEX)
    },
    2,       // Max number of channels
    16,      // Minimum number of bits per sample
    16,      // Maximum number of bits per channel
    44100,   // Minimum rate
    44100    // Maximum rate
  },

  // 48-kHz AC-3 over S/PDIF
  {
    {
      sizeof(KSDATARANGE_AUDIO),
      0,
      0,
      0,
      STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO),
      STATICGUIDOF(KSDATAFORMAT_SUBTYPE_AC3_SPDIF),
      STATICGUIDOF(KSDATAFORMAT_SPECIFIER_WAVEFORMATEX)
    },
    2,       // Max number of channels
    16,      // Minimum number of bits per sample
    16,      // Maximum number of bits per channel
    48000,   // Minimum rate
    48000    // Maximum rate
  },
};
```

在此代码示例中，第一个和第二个数据范围指定在 48khz 和 44.1 kHz 采样速率的 WMA Pro-反复-S/PDIF 数据格式。 有了这两个选项，音频应用程序可以播放 WMA Pro 音频流记录在这两个假设外部解码器还可以处理的采样率这些两个采样速率。

WMA Pro 同步帧大小是在 48khz 和 44.1 kHz 相同并使用同一个 PCM 参数值-两个通道，这两个数据区域和 16 位 / 通道。 有关使用 PCM 参数来指定 WMA Pro-反复-S/PDIF 和 AC-3-over-S/PDIF 格式的数据范围的信息，请参阅[S/PDIF 传递非 PCM 流的传输](s-pdif-pass-through-transmission-of-non-pcm-streams.md)。

第三个数据区域指定 AC-3-over-S/PDIF 数据格式。 有关详细信息，请参阅[指定 ac-3 数据范围](specifying-ac-3-data-ranges.md)。

前面的示例中不会启用 DirectSound 处理 PCM WMA Pro-反复-S/PDIF 和 AC-3-over-S/PDIF 格式可在 Microsoft Windows 2000 SP2 和 Windows 98 SE + 修补程序。 若要启用此功能，示例代码将需要修改，以便每三个数据区域使用说明符 KSDATAFORMAT\_说明符\_WAVEFORMATEX，第二个数据范围必须包含相同除外它使用说明符 KSDATAFORMAT\_说明符\_DSOUND 相反。 有关示例，请参阅[指定 ac-3 数据范围](specifying-ac-3-data-ranges.md)。

 

 




