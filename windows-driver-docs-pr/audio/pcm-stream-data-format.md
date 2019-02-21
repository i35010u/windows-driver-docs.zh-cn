---
title: PCM Stream 数据格式
description: PCM Stream 数据格式
ms.assetid: 86599e55-e771-4d6e-ad59-6dc905c53cd8
keywords:
- PCM 流数据格式 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 165a69f9b0efc90ab86fd70f1e8c59de4505dcb2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520182"
---
# <a name="pcm-stream-data-format"></a>PCM Stream 数据格式


## <span id="pcm_stream_data_format"></span><span id="PCM_STREAM_DATA_FORMAT"></span>


此示例使用[ **KSDATAFORMAT\_WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff537095)结构来描述 PCM 流的数据格式。

```cpp
  DataFormat.FormatSize  = sizeof(KSDATAFORMAT_WAVEFORMATEX);
  DataFormat.Flags       = 0;
  DataFormat.SampleSize  = 0;
  DataFormat.Reserved    = 0;
  DataFormat.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO);
  DataFormat.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_PCM);
 DataFormat.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_WAVEFORMATEX);
  Format.wFormatTag      = WAVE_FORMAT_PCM;
  Format.nChannels       = 2;
  Format.nSamplesPerSec  = 44100;
  Format.nAvgBytesPerSec = 176400;
  Format.nBlockAlign     = 4;
  Format.wBitsPerSample  = 16;
  Format.cbSize          = 0;
```

 

 




