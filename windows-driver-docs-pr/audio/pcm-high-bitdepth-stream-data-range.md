---
title: PCM 高位深度流数据范围
description: PCM 高位深度流数据范围
ms.assetid: 4f3d48ff-e01d-4c80-b493-253afdba6fd7
keywords:
- PCM bitdepth 流数据范围 WDK
- 高 bitdepth 流数据范围 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ab8662f746c0133d3528dae00c5e59e95c25a97
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210523"
---
# <a name="pcm-high-bitdepth-stream-data-range"></a>PCM 高位深度流数据范围


## <span id="pcm_high_bitdepth_stream_data_range"></span><span id="PCM_HIGH_BITDEPTH_STREAM_DATA_RANGE"></span>


此示例使用 [**KSDATARANGE \_ 音频**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio) 结构来描述 PCM bitdepth 流的数据范围。

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

此示例中的成员值与 [PCM 多通道流数据范围](pcm-multichannel-stream-data-range.md) 示例中的成员值相似，但 `MaximumBitsPerSample` 值除外，大于16。 此值设置为受支持的有效位的最大数目。 例如，如果设备支持24位容器中的20位有效音频数据，则的值 `MaximumBitsPerSample` 应设置为20。

 

