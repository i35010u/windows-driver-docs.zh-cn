---
title: PCM 多通道 Stream 数据范围
description: PCM 多通道 Stream 数据范围
ms.assetid: b7e1a5d9-fb8a-46ed-932b-d667e470d4ab
keywords:
- PCM 多渠道的流数据范围 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e612b8269af533472797cb0ed9efa569808ad1fd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548008"
---
# <a name="pcm-multichannel-stream-data-range"></a>PCM 多通道 Stream 数据范围


## <span id="pcm_multichannel_stream_data_range"></span><span id="PCM_MULTICHANNEL_STREAM_DATA_RANGE"></span>


此示例使用[ **KSDATARANGE\_音频**](https://msdn.microsoft.com/library/windows/hardware/ff537096)结构来描述 PCM 多通道流的数据范围。

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
  MaximumBitsPerSample   = 16;
  MinimumSampleFrequency = 5000;
  MaximumSampleFrequency = 48000;
```

 

 




