---
title: PCM 高位深度流数据范围
description: PCM 高位深度流数据范围
ms.assetid: 4f3d48ff-e01d-4c80-b493-253afdba6fd7
keywords:
- PCM 高 bitdepth 流数据范围 WDK
- 高 bitdepth 流数据范围 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42628b45256d8b1ec85d9599fd3a7118815b8e6f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566301"
---
# <a name="pcm-high-bitdepth-stream-data-range"></a>PCM 高位深度流数据范围


## <span id="pcm_high_bitdepth_stream_data_range"></span><span id="PCM_HIGH_BITDEPTH_STREAM_DATA_RANGE"></span>


此示例使用[ **KSDATARANGE\_音频**](https://msdn.microsoft.com/library/windows/hardware/ff537096)结构来描述 PCM 高 bitdepth 流的数据范围。

```cpp
  DataRange.FormatSize  = sizeof(KSDATARANGE_AUDIO);
  DataRange.Flags       = 0;
  DataRange.SampleSize  = 0;
  DataRange.Reserved    = 0;
  DataRange.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO);
  DataRange.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_PCM);
  DataRange.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_WAVEFORMATEX);
  MaximumChannels        = 4;   // max number of channels, or -1 for unlimited
  MinimumBitsPerSample   = 2;
  MaximumBitsPerSample   = 24;  // 24, 32, etc.
  MinimumSampleFrequency = 5000;
  MaximumSampleFrequency = 48000;
```

在此示例中的成员值是类似于中的那些[PCM 多通道 Stream 数据范围](pcm-multichannel-stream-data-range.md)示例中的，除`MaximumBitsPerSample`值，该值大于 16。 此值设置为支持的有效位数的最大数目。 例如，如果设备支持 24 位容器中，为值的有效的音频数据的 20 位`MaximumBitsPerSample`应设置为 20。

 

 




