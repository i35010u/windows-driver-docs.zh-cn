---
title: DirectSound 流数据范围
description: DirectSound 流数据范围
ms.assetid: cc31eb2d-7421-4748-b14c-f4d3d15f9884
keywords:
- DirectSound WDK 音频，流数据范围
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12eebfffc9b53a3770eaeb47247fb9dda58ea38a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333762"
---
# <a name="directsound-stream-data-range"></a>DirectSound 流数据范围


## <span id="directsound_stream_data_range"></span><span id="DIRECTSOUND_STREAM_DATA_RANGE"></span>


此示例使用[ **KSDATARANGE\_音频**](https://msdn.microsoft.com/library/windows/hardware/ff537096)结构来描述 DirectSound 流的数据范围。

```cpp
  DataRange.FormatSize  = sizeof(KSDATARANGE_AUDIO);
  DataRange.Flags       = 0;
  DataRange.SampleSize  = 0;
  DataRange.Reserved    = 0;
  DataRange.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO);
  DataRange.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_PCM);
  DataRange.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_DSOUND);
  MaximumChannels        = 4;   // max number of channels, or -1 for unlimited
  MinimumBitsPerSample   = 2;
  MaximumBitsPerSample   = 16;  // 16, 24, 32, etc.
  MinimumSampleFrequency = 5000;
  MaximumSampleFrequency = 48000;
```

在此示例中的成员值是类似于[PCM 多渠道的流数据范围](pcm-multichannel-stream-data-range.md)示例中的，除**MaximumBitsPerSample**值。 此值设置为示例容器大小，并且应为八的倍数。 例如，如果设备支持 24 位容器中，为值的有效的音频数据的 20 位**MaximumBitsPerSample**应设置为 24。

 

 




