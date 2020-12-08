---
title: PCM 流数据格式
description: PCM 流数据格式
keywords:
- PCM 流数据格式 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27b4f3aacdf247a09711605237e5df229473383a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800955"
---
# <a name="pcm-stream-data-format"></a>PCM 流数据格式


## <span id="pcm_stream_data_format"></span><span id="PCM_STREAM_DATA_FORMAT"></span>


此示例使用 [**KSDATAFORMAT \_ WAVEFORMATEX**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex) 结构来描述 PCM 流的数据格式。

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

 

