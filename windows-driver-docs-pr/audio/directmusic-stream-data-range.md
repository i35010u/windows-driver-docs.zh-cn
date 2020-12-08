---
title: DirectMusic 流数据范围
description: DirectMusic 流数据范围
keywords:
- DirectMusic WDK 音频，流数据范围
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3df07a4a9ed8d5756d2e77ad78a58adeb6a01717
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789283"
---
# <a name="directmusic-stream-data-range"></a>DirectMusic 流数据范围


## <span id="directmusic_stream_data_range"></span><span id="DIRECTMUSIC_STREAM_DATA_RANGE"></span>


此示例使用 [**KSDATARANGE \_ 音乐**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_music) 结构来描述 DirectMusic 流的数据范围。

```cpp
  DataRange.FormatSize  = sizeof(KSDATARANGE_MUSIC);
 DataRange.Flags       = 0;
  DataRange.SampleSize  = 0;
  DataRange.Reserved    = 0;
 DataRange.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_MUSIC);
  DataRange.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_DIRECTMUSIC);
  DataRange.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_NONE);
  Technology            = STATICGUIDOF(KSMUSIC_TECHNOLOGY_WAVETABLE);
  Channels              = 0;
  Notes                 = 0;
  ChannelMask           = 0xFFFF;
```

 

