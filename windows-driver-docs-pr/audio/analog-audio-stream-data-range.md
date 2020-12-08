---
title: 模拟音频流数据范围
description: 模拟音频流数据范围
keywords:
- 模拟音频 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 878b641f22a6b7600f94c04d7ef2e97ad32e9009
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789445"
---
# <a name="analog-audio-stream-data-range"></a>模拟音频流数据范围


## <span id="analog_audio_stream_data_range"></span><span id="ANALOG_AUDIO_STREAM_DATA_RANGE"></span>


此示例使用 [**KSDATARANGE**](/previous-versions/ff561658(v=vs.85)) 结构来描述模拟音频流的数据范围。

```cpp
  DataRange.FormatSize  = sizeof(KSDATARANGE);
  DataRange.Flags       = 0;
  DataRange.SampleSize  = 0;
  DataRange.Reserved    = 0;
  DataRange.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO);
  DataRange.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_ANALOG);
  DataRange.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_NONE);
```

通常，微型端口驱动程序使用这种类型的数据范围来描述通过 *桥接* 的模拟信号，该信号表示音频适配器卡上的硬编码连接。 有关桥接 pin 的详细信息，请参阅 [音频筛选器图](audio-filter-graphs.md)。 另请参阅 [公开筛选器拓扑](exposing-filter-topology.md)中的代码示例。

 

