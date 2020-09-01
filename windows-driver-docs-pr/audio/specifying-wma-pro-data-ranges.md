---
title: 指定 WMA Pro 数据范围
description: 指定 WMA Pro 数据范围
ms.assetid: c7e9bc68-cec2-4a34-9ef0-ce3c9a4cc987
keywords:
- S/PDIF 传递 WDK 音频
- WMA Pro-S/PDIF 格式 WDK 音频
- 音频非 PCM 格式 WDK
- 非 PCM 音频格式 WDK，S/PDIF
- WMA Pro WDK 音频
- 索尼/Philips 数字接口
- 数据范围 WDK 音频、WMA Pro
- 非 PCM 音频格式 WDK、WMA Pro
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b9ff66e77c5d1688829ed83eef753e97edbe89d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210383"
---
# <a name="specifying-wma-pro-data-ranges"></a>指定 WMA Pro 数据范围


## <span id="specifying_wma_pro_data_ranges"></span><span id="SPECIFYING_WMA_PRO_DATA_RANGES"></span>


标头文件 Mmreg 将值0x0164 定义为 WMA-over S/PDIF 的波形格式标记：

```cpp
  #define WAVE_FORMAT_WMASPDIF  0x0164
```

可以使用 \_ 标头文件 Ksmedia 中的 DEFINE WAVEFORMATEX guid 宏，按波形格式标记指定对应的格式子类型 guid \_ ，如下所示：

```cpp
  #define KSDATAFORMAT_SUBTYPE_WMA_SPDIF    \
                      DEFINE_WAVEFORMATEX_GUID(WAVE_FORMAT_WMASPDIF)
```

下面的代码示例演示了 WaveCyclic 或 WavePci 微型端口驱动程序如何为支持/PDIF 和 AC-3/PDIF 格式的 pin 指定 [**KSDATARANGE \_ 音频**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio) 表条目：

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

在此代码示例中，第一个和第二个数据区域以 48 kHz 和 44.1 kHz 的采样速率指定 WMA Pro-S/PDIF 数据格式。 使用这两个选项，音频应用程序可以播放在这两个采样速率中记录的 WMA Pro 音频流，假设外部解码器还可以处理采样速率。

WMA Pro 同步帧大小在 48 kHz 和 44.1 kHz 均相同，并且这两个数据区域都使用相同的 PCM 参数值-两个通道和16位/通道。 若要了解如何使用 PCM 参数来指定 WMA Pro over S/PDIF 和 AC-3/PDIF 格式的数据范围，请参阅 [非 PCM 流的 S/Pdif 传递传输](s-pdif-pass-through-transmission-of-non-pcm-streams.md)。

第三个数据区域指定 AC-3-S/PDIF 数据格式。 有关详细信息，请参阅 [指定 AC 3 数据范围](specifying-ac-3-data-ranges.md)。

前面的示例不允许 DirectSound 在 Microsoft Windows 2000 SP2 和 Windows 98 SE + 修补程序上处理非 PCM WMA Pro over S/PDIF 和 AC-3/PDIF 格式。 若要启用此功能，需要修改示例代码，以便对于使用说明符 KSDATAFORMAT 说明符 WAVEFORMATEX 的三个数据范围中的每个数据区域 \_ \_ ，必须包含相同的另一个数据范围，只不过它使用说明符 KSDATAFORMAT \_ 说明符 \_ DSOUND。 有关示例，请参阅 [指定 AC 3 数据范围](specifying-ac-3-data-ranges.md)。

 

