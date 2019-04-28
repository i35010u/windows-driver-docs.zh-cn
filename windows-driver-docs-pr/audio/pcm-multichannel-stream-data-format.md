---
title: PCM 多声道流数据格式
description: PCM 多声道流数据格式
ms.assetid: cab528a7-5db4-4e37-89c4-35dfc472f0ae
keywords:
- PCM 多渠道的流数据格式 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afe5949b7f3049df52ebc7d0f3390430a821e03b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332231"
---
# <a name="pcm-multichannel-stream-data-format"></a>PCM 多声道流数据格式


## <span id="pcm_multichannel_stream_data_format"></span><span id="PCM_MULTICHANNEL_STREAM_DATA_FORMAT"></span>


此示例使用的扩展的版本[ **KSDATAFORMAT\_WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff537095)结构来描述 PCM 多通道流的数据格式。

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
  Format.nAvgBytesPerSec = 352800;
  Format.nBlockAlign     = 8;
  Format.wBitsPerSample  = 16;
  Format.cbSize          = sizeof(WAVEFORMATEXTENSIBLE) - sizeof(WAVEFORMATEX);
  Format.wValidBitsPerSample = 16;
  Format.dwChannelMask   = KSAUDIO_SPEAKER_SURROUND;
  Format.SubFormat       = KSDATAFORMAT_SUBTYPE_PCM;
```

 

 




