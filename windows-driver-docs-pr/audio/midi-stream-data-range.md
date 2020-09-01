---
title: MIDI 流数据范围
description: MIDI 流数据范围
ms.assetid: 392eadf7-9c6e-4527-bc84-a2916623c154
keywords:
- MIDI 流数据范围 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85630cb68323fb8c9f9b09e8292a2ecdb09d7970
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211389"
---
# <a name="midi-stream-data-range"></a>MIDI 流数据范围


## <span id="midi_stream_data_range"></span><span id="MIDI_STREAM_DATA_RANGE"></span>


此示例使用 [**KSDATARANGE \_ 音乐**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_music) 结构来描述 MIDI 流的数据范围。

```cpp
  DataRange.FormatSize  = sizeof(KSDATARANGE_MUSIC);
 DataRange.Flags       = 0;
  DataRange.SampleSize  = 0;
  DataRange.Reserved    = 0;
 DataRange.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_MUSIC);
  DataRange.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_MIDI);
  DataRange.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_NONE);
  Technology            = STATICGUIDOF(KSMUSIC_TECHNOLOGY_PORT);
  Channels              = 0;
  Notes                 = 0;
  ChannelMask           = 0xFFFF;
```

 

