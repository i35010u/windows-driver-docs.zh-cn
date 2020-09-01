---
title: 模拟音频流数据范围
description: 模拟音频流数据范围
ms.assetid: e4503ace-1e96-401e-b410-18ee6b07a37b
keywords:
- 模拟音频 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 936ad866e1e3c5669d4cec588e7fd85221a3e2a3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208369"
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

通常，微型端口驱动程序使用这种类型的数据范围来描述通过 *桥接*的模拟信号，该信号表示音频适配器卡上的硬编码连接。 有关桥接 pin 的详细信息，请参阅 [音频筛选器图](audio-filter-graphs.md)。 另请参阅 [公开筛选器拓扑](exposing-filter-topology.md)中的代码示例。

 

