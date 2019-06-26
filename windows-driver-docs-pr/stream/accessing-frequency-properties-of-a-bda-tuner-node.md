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
ms.openlocfilehash: 2cc168e3567960eb95d0584d19545e399b059971
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386778"
---
# <a name="accessing-frequency-properties-of-a-bda-tuner-node"></a>访问 BDA 调谐器节点的频率属性





使用网络提供商[KSPROPSETID\_BdaFrequencyFilter](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-bdafrequencyfilter)属性设置来控制 RF 调谐器拓扑中某节点 BDA 筛选器。 例如，网络提供商使用此属性设置为告知如何优化 RF 信号的调谐器节点。

下面的代码段，控制 BDA 微型驱动程序中的调谐器节点的 pin 截获，并提供了用于 KSPROPSETID 属性方法\_BdaFrequencyFilter 属性集。 请注意，某些 KSPROPSETID\_BdaFrequencyFilter 属性都只适用于特定类型的调谐器。

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

 

 




