---
title: DirectMusic Stream 数据范围
description: DirectMusic Stream 数据范围
ms.assetid: e3423901-330e-4a86-a921-6678e1c45a97
keywords:
- DirectMusic WDK 音频，流数据范围
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad971162c43bced5fafb190b65dc5ed3ad5f0e53
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548249"
---
# <a name="directmusic-stream-data-range"></a>DirectMusic Stream 数据范围


## <span id="directmusic_stream_data_range"></span><span id="DIRECTMUSIC_STREAM_DATA_RANGE"></span>


此示例使用[ **KSDATARANGE\_音乐**](https://msdn.microsoft.com/library/windows/hardware/ff537097)结构来描述 DirectMusic 流的数据范围。

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

 

 




