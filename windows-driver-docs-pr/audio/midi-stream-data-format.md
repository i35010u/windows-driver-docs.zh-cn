---
title: MIDI Stream 数据格式
description: MIDI Stream 数据格式
ms.assetid: c179cf74-7493-4c27-97bd-5eb4d0dffbe6
keywords:
- MIDI 数据格式 WDK 音频进行流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1edb84cf06c56e713dc9f41d3297e68a25efa447
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534243"
---
# <a name="midi-stream-data-format"></a>MIDI Stream 数据格式


## <span id="midi_stream_data_format"></span><span id="MIDI_STREAM_DATA_FORMAT"></span>


此示例使用[ **KSDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff561656)结构来描述 MIDI 流的数据格式。

```cpp
  DataFormat.FormatSize  = sizeof(KSDATAFORMAT);
  DataFormat.Flags       = 0;
  DataFormat.SampleSize  = 0;
 DataFormat.Reserved    = 0;
  DataFormat.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_MUSIC);
  DataFormat.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_MIDI);
  DataFormat.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_NONE);
```

 

 




