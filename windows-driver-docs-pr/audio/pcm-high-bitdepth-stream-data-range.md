---
title: PCM 高位深度流数据范围
description: PCM 高位深度流数据范围
ms.assetid: 4f3d48ff-e01d-4c80-b493-253afdba6fd7
keywords:
- PCM bitdepth 流数据范围 WDK
- 高 bitdepth 流数据范围 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2852f62f95b0792f8e39583b7da377acdfaddcb2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830264"
---
# <a name="pcm-high-bitdepth-stream-data-range"></a>PCM 高位深度流数据范围


## <span id="pcm_high_bitdepth_stream_data_range"></span><span id="PCM_HIGH_BITDEPTH_STREAM_DATA_RANGE"></span>


此示例使用[**KSDATARANGE\_音频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)结构来描述 PCM bitdepth 流的数据范围。

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

本示例中的成员值类似于[PCM 多通道流数据范围](pcm-multichannel-stream-data-range.md)示例中的成员值，`MaximumBitsPerSample` 值除外，大于16。 此值设置为受支持的有效位的最大数目。 例如，如果设备支持24位容器中的20位有效音频数据，则 `MaximumBitsPerSample` 的值应设置为20。

 

 




