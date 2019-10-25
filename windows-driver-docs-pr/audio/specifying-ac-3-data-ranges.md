---
title: 指定 AC-3 数据范围
description: 指定 AC-3 数据范围
ms.assetid: 87d59554-43fa-4d61-9829-c38691d0a525
keywords:
- S/PDIF 传递 WDK 音频
- AC-3-S/PDIF 格式 WDK 音频
- 音频非 PCM 格式 WDK
- 非 PCM 音频格式 WDK，S/PDIF
- WMA Pro WDK 音频
- AC 3 WDK 音频
- 索尼/Philips 数字接口
- 数据范围 WDK 音频、AC-3
- 非 PCM 音频格式 WDK、AC 3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e7fd788269cc3c571a72e1190875aa7e836c177
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830115"
---
# <a name="specifying-ac-3-data-ranges"></a>指定 AC-3 数据范围


## <span id="specifying_ac_3_data_ranges"></span><span id="SPECIFYING_AC_3_DATA_RANGES"></span>


标头文件 Mmreg 将值0x0092 定义为 AC-3/PDIF 的波形格式标记：

```cpp
    #define WAVE_FORMAT_DOLBY_AC3_SPDIF  0x0092
```

波形格式标记0x0240 和0x0241 与0x0092 同义，许多 DVD 应用程序将三个标记视为相同。 但是，为了消除冗余，驱动程序和应用程序应仅支持标记0x0092 （而不支持标记0x0240 和0x0241）。

可以通过使用标头文件 Ksmedia 中的 "定义\_WAVEFORMATEX"\_GUID 宏，按波形格式标记指定对应的格式子类型 GUID，如下所示：

```cpp
  #define KSDATAFORMAT_SUBTYPE_AC3_SPDIF    \
                      DEFINE_WAVEFORMATEX_GUID(WAVE_FORMAT_DOLBY_AC3_SPDIF)
```

下面的代码示例演示了 WaveCyclic 或 WavePci 微型端口驱动程序如何为支持 AC-3/PDIF 格式的 pin 指定[**KSDATARANGE\_音频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)表条目：

```cpp
static KSDATARANGE_AUDIO PinDataRangesAC3Stream[] =
{
  // 48-kHz AC-3 over S/PDIF
  {
    {
      sizeof(KSDATARANGE_AUDIO),
      0,
      0,
      0,
      STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO),
      STATICGUIDOF(KSDATAFORMAT_SUBTYPE_DOLBY_AC3_SPDIF),
      STATICGUIDOF(KSDATAFORMAT_SPECIFIER_WAVEFORMATEX)
    },
    2,     // Max number of channels
    16,    // Minimum number of bits per sample
    16,    // Maximum number of bits per channel
    48000, // Minimum rate
    48000  // Maximum rate
  },

  // If you do not include this second data range (which is identical
  // to the first except for the value KSDATAFORMAT_SPECIFIER_DSOUND),
  // then your non-PCM pin is not seen by DirectSound on Windows 98 SE
  // or Windows 2000, regardless of the DirectX version or whether a
  // hotfix or service pack is installed.
  {
    {
      sizeof(KSDATARANGE_AUDIO),
      0,
      0,
      0,
      STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO),
      STATICGUIDOF(KSDATAFORMAT_SUBTYPE_DOLBY_AC3_SPDIF),
      STATICGUIDOF(KSDATAFORMAT_SPECIFIER_DSOUND)
    },
    2,     // Max number of channels
    16,    // Minimum number of bits per sample
    16,    // Maximum number of bits per channel
    48000, // Minimum rate
    48000  // Maximum rate
  }
};
```

上表中的第二个数据范围条目对于启用 DirectSound 以处理 Windows 2000 SP2 和 Microsoft Windows 98 SE + 修补程序中的非 PCM AC-3/PDIF 格式是必需的。

对于微型端口驱动程序使用 KSDATAFORMAT\_说明符指定的每个数据范围\_WAVEFORMATEX，端口驱动程序会自动添加另一个使用 KSDATAFORMAT\_说明符指定的数据范围\_DSOUND，但否则与第一个相同。 （您可以使用[KsStudio 实用工具](ksstudio-utility.md)来查看数据范围的列表。）在 Windows 2000 和 Windows 98 中，端口驱动程序只为 KSDATAFORMAT\_子类型创建 KSDATAFORMAT\_说明符\_DSOUND 版本\_PCM 格式，因为 DirectSound 8 之前的 DirectSound 版本仅支持 PCM。 此限制在 Windows XP 和更高版本以及 Windows Me 中被删除。 但是，它不会在 Windows 2000 SP2 或 Windows 98 SE 的热修复包中删除，并且在这些 Windows 版本的 DirectSound 上支持非 PCM，驱动程序应为每个非 PCM 数据格式显式列出两个数据范围-一个使用 KSDATAFORMAT\_说明符\_WAVEFORMATEX，另一个具有 KSDATAFORMAT\_说明符\_DSOUND。

正如通过[非 PCM 流的 S/PDIF 直通传输](s-pdif-pass-through-transmission-of-non-pcm-streams.md)中所述，两个 AC-3 个/PDIF 数据范围均使用以下 PCM 参数：两个通道，每个通道16位。

 

 




