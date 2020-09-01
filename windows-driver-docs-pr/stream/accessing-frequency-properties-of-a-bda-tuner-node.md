---
title: 访问 BDA 调谐器节点的频率属性
description: 访问 BDA 调谐器节点的频率属性
ms.assetid: 47c24e99-c82c-4bc8-af36-bd7f728634ba
keywords:
- 方法设置 WDK BDA，RF 调谐器节点
- 属性设置 WDK BDA，RF 调谐器节点
- KSPROPSETID_BdaFrequencyFilter
- RF 调谐器 WDK BDA
- 频率属性 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44788878ce12d3e25b5b37ff7e7d3b1d4d4f75eb
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184633"
---
# <a name="accessing-frequency-properties-of-a-bda-tuner-node"></a>访问 BDA 调谐器节点的频率属性





网络提供程序使用 [KSPROPSETID \_ BdaFrequencyFilter](./kspropsetid-bdafrequencyfilter.md) 属性集来控制 BDA 筛选器拓扑中的 RF 调谐器节点。 例如，网络提供程序使用此属性集来告知调谐器节点如何调整 RF 信号。

在以下代码片段中，"BDA 微型驱动程序中的调谐器" 节点的控制 pin 会截获并提供 KSPROPSETID BdaFrequencyFilter 属性集的属性的方法 \_ 。 请注意，有些 KSPROPSETID \_ BdaFrequencyFilter 属性仅适用于特定类型的调谐器。

```cpp
//
//  BDA RF Tune Frequency Filter
//
//  Defines the dispatch routines for the Properties
//  on the RF Tuner Node
//
DEFINE_KSPROPERTY_TABLE(RFNodeFrequencyProperties)
{
    DEFINE_KSPROPERTY_ITEM_BDA_RF_TUNER_FREQUENCY(
        CAntennaPin::GetCenterFrequency,
        CAntennaPin::PutCenterFrequency
        ),
    DEFINE_KSPROPERTY_ITEM_BDA_RF_TUNER_FREQUENCY_MULTIPLIER(
        NULL,
        CAntennaPin::PutFrequencyMultiplier // If this set handler 
        // is not called, the minidriver must determine that the 
        // frequency is in kHz. That is, the default multiplier is 
        // 1000 (1Hz x 1000).
        ),
#ifdef SATELLITE_TUNER // Only applicable to satellite tuners.
    DEFINE_KSPROPERTY_ITEM_BDA_RF_TUNER_POLARITY(
        NULL, NULL
        ),
    DEFINE_KSPROPERTY_ITEM_BDA_RF_TUNER_RANGE(
        NULL, NULL
        ),
#endif // SATELLITE_TUNER
#ifdef CHANNEL_BASED_TUNER // Only applicable to channel-based tuners.
    DEFINE_KSPROPERTY_ITEM_BDA_RF_TUNER_TRANSPONDER(
        NULL, NULL
        ),
#endif // CHANNEL_BASED_TUNER
#ifdef DVBT_TUNER // Only applicable to tuners that tune Digital Video Broadcast (DVB) signals.
    DEFINE_KSPROPERTY_ITEM_BDA_RF_TUNER_BANDWIDTH(
        NULL, NULL
        ),
#endif // DVBT_TUNER
};
```

 

