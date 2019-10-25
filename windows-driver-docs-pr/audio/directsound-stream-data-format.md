---
title: DirectSound 流数据格式
description: DirectSound 流数据格式
ms.assetid: 41d3d5ad-7336-4ecf-b6e2-a24ee4ec731f
keywords:
- DirectSound WDK 音频，流数据格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 295a791b9d625b9e8a710743ff2df23bcd949e75
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833496"
---
# <a name="directsound-stream-data-format"></a>DirectSound 流数据格式


## <span id="directsound_stream_data_format"></span><span id="DIRECTSOUND_STREAM_DATA_FORMAT"></span>


此示例使用[**KSDATAFORMAT\_DSOUND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_dsound)结构来描述 DirectSound 流的数据格式。

```cpp
  DataFormat.FormatSize  = sizeof(KSDATAFORMAT_DSOUND);
 DataFormat.Flags       = 0;
  DataFormat.SampleSize  = 0;
  DataFormat.Reserved    = 0;
  DataFormat.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO);
  DataFormat.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_PCM);
 DataFormat.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_DSOUND);
  BufferDesc.Flags       = KSDSOUND_BUFFER_LOCHARDWARE;
  BufferDesc.Control     = KSDSOUND_BUFFER_CTRL_3D;
  BufferDesc.WaveFormatEx.wFormatTag      = WAVE_FORMAT_PCM;
  BufferDesc.WaveFormatEx.nChannels       = 2;
  BufferDesc.WaveFormatEx.nSamplesPerSec  = 22050;
  BufferDesc.WaveFormatEx.nAvgBytesPerSec = 88200;
  BufferDesc.WaveFormatEx.nBlockAlign     = 4;
  BufferDesc.WaveFormatEx.wBitsPerSample  = 16;
  BufferDesc.WaveFormatEx.cbSize          = 0;
```

 

 




