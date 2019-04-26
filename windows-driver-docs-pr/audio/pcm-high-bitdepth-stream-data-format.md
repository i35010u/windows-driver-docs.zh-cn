---
title: PCM 高位深度流数据格式
description: PCM 高位深度流数据格式
ms.assetid: 0ad63f01-4fcf-4eca-b8d6-b0b65f384455
keywords:
- PCM 高 bitdepth 流数据格式 WDK
- 高 bitdepth 流数据格式 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4bcaf4ab83d2e0d5c945240d5de894713fbc7c0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332239"
---
# <a name="pcm-high-bitdepth-stream-data-format"></a>PCM 高位深度流数据格式


## <span id="pcm_high_bitdepth_stream_data_format"></span><span id="PCM_HIGH_BITDEPTH_STREAM_DATA_FORMAT"></span>


此示例使用的扩展的版本[ **KSDATAFORMAT\_WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff537095)结构来描述 PCM 高 bitdepth 流的数据格式。 这是类似于 PCM 多渠道示例的值除外`Format.wBitsPerSample`和`Format.wValidBitsPerSample`下面显示的。

```cpp
  DataFormat.FormatSize  = sizeof(KSDATAFORMAT) + sizeof(WAVEFORMATEXTENSIBLE);
 DataFormat.Flags       = 0;
  DataFormat.SampleSize  = 0;
  DataFormat.Reserved    = 0;
  DataFormat.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO);
  DataFormat.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_PCM);
 DataFormat.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_WAVEFORMATEX);
  Format.wFormatTag      = WAVE_FORMAT_EXTENSIBLE;
  Format.nChannels       = 4;
  Format.nSamplesPerSec  = 44100;
  Format.nAvgBytesPerSec = 529200;
  Format.nBlockAlign     = 8;
  Format.wBitsPerSample  = 24;
  Format.cbSize          = sizeof(WAVEFORMATEXTENSIBLE) - sizeof(WAVEFORMATEX);
  Format.wValidBitsPerSample = 20;
  Format.dwChannelMask   = KSAUDIO_SPEAKER_SURROUND;
  Format.SubFormat       = KSDATAFORMAT_SUBTYPE_PCM;
```

 

 




