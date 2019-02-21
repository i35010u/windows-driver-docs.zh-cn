---
title: 指定 ac-3 数据范围
description: 指定 ac-3 数据范围
ms.assetid: 87d59554-43fa-4d61-9829-c38691d0a525
keywords:
- S/PDIF 传递 WDK 音频
- AC-3-over-S/PDIF 格式 WDK 音频
- 音频非 PCM 格式 WDK
- 非 PCM 音频格式 WDK、 S/PDIF
- WMA Pro WDK 音频
- Ac-3 WDK 音频
- 索尼/菲利普数字接口
- 数据范围 WDK 音频 ac-3
- 非 PCM 音频格式 WDK、 ac-3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6b9480e9ad1d81af5d547f57bbe1f0f4ddfc70d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546361"
---
# <a name="specifying-ac-3-data-ranges"></a>指定 ac-3 数据范围


## <span id="specifying_ac_3_data_ranges"></span><span id="SPECIFYING_AC_3_DATA_RANGES"></span>


标头文件 Mmreg.h 定义 0x0092 AC-3-over-S/PDIF 波形格式标记的值：

```cpp
    #define WAVE_FORMAT_DOLBY_AC3_SPDIF  0x0092
```

波形格式标记 0x0240 和 0x0241 是 0x0092 的同义词，并且许多 DVD 应用程序将三个标记视为相同。 但是，若要消除冗余，驱动程序和应用程序应支持仅标记 0x0092 （和不支持标记 0x0240 和 0x0241）。

可以通过使用定义方面波形格式标记指定相应的子类型格式的 GUID\_WAVEFORMATEX\_标头中的 GUID 宏文件 Ksmedia.h，如下所示：

```cpp
  #define KSDATAFORMAT_SUBTYPE_AC3_SPDIF    \
                      DEFINE_WAVEFORMATEX_GUID(WAVE_FORMAT_DOLBY_AC3_SPDIF)
```

以下代码示例演示如何指定 WaveCyclic 或 WavePci 微型端口驱动程序[ **KSDATARANGE\_音频**](https://msdn.microsoft.com/library/windows/hardware/ff537096)表支持 AC-3-over-S/PDIF 格式 pin 条目：

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

上表中的第二个数据区域项，才可启用 DirectSound 以处理非 PCM AC-3-over-S/PDIF 格式在 Windows 2000 SP2 和在 Microsoft Windows 98 SE + 修补程序。

为每个与 KSDATAFORMAT 微型端口驱动程序指定的数据范围\_说明符\_WAVEFORMATEX，端口驱动程序会自动添加使用 KSDATAFORMAT 指定第二个数据范围\_说明符\_DSOUND 但在其他方面与第一个。 (您可以通过使用对此进行验证[KsStudio 实用工具](ksstudio-utility.md)若要查看的数据范围列表。)在 Windows 2000 和 Windows 98，端口驱动程序创建 KSDATAFORMAT\_说明符\_DSOUND 版本的数据范围仅 KSDATAFORMAT\_子类型\_PCM 格式因为 DirectSound 之前的版本DirectSound 8 支持仅 PCM。 这一限制是在 Windows XP 中已删除和更高版本以及在 Windows me 一起提供。 但是，它不会删除在 Windows 2000 SP2 或 Windows 98 SE 修补程序包中，若要支持非 PCM 上 DirectSound 这些 Windows 版本上，驱动程序应显式列出的每个非 PCM 数据格式，那么，另一个使用 KSDATAFORMAT两个数据区域\_说明符\_WAVEFORMATEX，另一个具有 KSDATAFORMAT\_说明符\_DSOUND。

中所述[S/PDIF 传递非 PCM 流的传输](s-pdif-pass-through-transmission-of-non-pcm-streams.md)，两个 AC-3-over-S/PDIF 数据范围这两个使用以下 PCM 参数： 两个通道和 16 位 / 通道。

 

 




