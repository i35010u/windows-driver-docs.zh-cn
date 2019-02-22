---
title: 模拟音频 Stream 数据范围
description: 模拟音频 Stream 数据范围
ms.assetid: e4503ace-1e96-401e-b410-18ee6b07a37b
keywords:
- 模拟音频 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c15f3ceab899ca3c3d4c965df5aa85a08da507c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524018"
---
# <a name="analog-audio-stream-data-range"></a>模拟音频 Stream 数据范围


## <span id="analog_audio_stream_data_range"></span><span id="ANALOG_AUDIO_STREAM_DATA_RANGE"></span>


此示例使用[ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)结构来描述模拟音频流的数据范围。

```cpp
  DataRange.FormatSize  = sizeof(KSDATARANGE);
  DataRange.Flags       = 0;
  DataRange.SampleSize  = 0;
  DataRange.Reserved    = 0;
  DataRange.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO);
  DataRange.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_ANALOG);
  DataRange.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_NONE);
```

微型端口驱动程序通常情况下，使用这种类型的数据范围来描述通过模拟信号*桥 pin*，表示音频的适配器卡上的硬编码连接。 有关桥的 pin 的详细信息，请参阅[音频筛选器关系图](audio-filter-graphs.md)。 此外，请参阅中的代码示例[公开筛选器拓扑](exposing-filter-topology.md)。

 

 




