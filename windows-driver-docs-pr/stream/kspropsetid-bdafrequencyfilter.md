---
title: KSPROPSETID \_ BdaFrequencyFilter
description: KSPROPSETID \_ BdaFrequencyFilter
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aad51e36a0d5a3e3b61046dfe895738867166066
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837841"
---
# <a name="kspropsetid_bdafrequencyfilter"></a>KSPROPSETID \_ BdaFrequencyFilter


## <span id="ddk_kspropsetid_bdafrequencyfilter_ks"></span><span id="DDK_KSPROPSETID_BDAFREQUENCYFILTER_KS"></span>


KSPROPSETID \_ BdaFrequencyFilter 为 BDA frequency filter 属性集。 它用于控制接收方拓扑中的 RF 调谐器节点。

以下属性可用：

<span id="KSPROPERTY_BDA_RF_TUNER_FREQUENCY"></span><span id="ksproperty_bda_rf_tuner_frequency"></span>[**KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ 频率**](ksproperty-bda-rf-tuner-frequency.md)  
向调谐器节点通知信号托架的基本频率。 使用 KSPROPERTY BDA RF 射频乘数属性的值乘以基准频率 \_ \_ \_ \_ \_ ，以获得实际的频率。

<span id="KSPROPERTY_BDA_RF_TUNER_POLARITY"></span><span id="ksproperty_bda_rf_tuner_polarity"></span>[**KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ 极性**](ksproperty-bda-rf-tuner-polarity.md)  
通知调谐器节点有关传输的信号使用的 polarization。

<span id="KSPROPERTY_BDA_RF_TUNER_RANGE"></span><span id="ksproperty_bda_rf_tuner_range"></span>[**KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ 范围**](ksproperty-bda-rf-tuner-range.md)  
设置调谐器范围。

<span id="KSPROPERTY_BDA_RF_TUNER_TRANSPONDER"></span><span id="ksproperty_bda_rf_tuner_transponder"></span>[**KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ TRANSPONDER**](ksproperty-bda-rf-tuner-transponder.md)  
向调谐器节点通知相应的 transponder 号。

<span id="KSPROPERTY_BDA_RF_TUNER_BANDWIDTH"></span><span id="ksproperty_bda_rf_tuner_bandwidth"></span>[**KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ 带宽**](ksproperty-bda-rf-tuner-bandwidth.md)  
将传输的信号的带宽通知给调谐器节点。

<span id="KSPROPERTY_BDA_RF_TUNER_FREQUENCY_MULTIPLIER"></span><span id="ksproperty_bda_rf_tuner_frequency_multiplier"></span>[**KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ 频率 \_ 乘数**](ksproperty-bda-rf-tuner-frequency-multiplier.md)  
向调谐器节点通知 KSPROPERTY \_ BDA \_ RF \_ 调谐器 FREQUENCY 属性的值， \_ 以获取实际频率。

### <a name="comments"></a>注释

KSPROPSETID \_ BdaFrequencyFilter 属性集在几乎所有调谐器之间是通用的。 它用于通知调谐器节点如何调整 RF 信号。

 

 





