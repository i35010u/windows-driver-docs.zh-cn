---
title: KSPROPSETID\_BdaFrequencyFilter
description: KSPROPSETID\_BdaFrequencyFilter
ms.assetid: 7650a239-3d49-4cb1-99bb-12bac55d70d2
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82ced82098e7dc6dd5deaf0c711266ec0b2463ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525184"
---
# <a name="kspropsetidbdafrequencyfilter"></a>KSPROPSETID\_BdaFrequencyFilter


## <span id="ddk_kspropsetid_bdafrequencyfilter_ks"></span><span id="DDK_KSPROPSETID_BDAFREQUENCYFILTER_KS"></span>


KSPROPSETID\_BdaFrequencyFilter 未 BDA 频率设置筛选器属性。 它用于控制 RF 调谐器节点接收方拓扑中。

可用属性如下：

<span id="KSPROPERTY_BDA_RF_TUNER_FREQUENCY"></span><span id="ksproperty_bda_rf_tuner_frequency"></span>[**KSPROPERTY\_BDA\_RF\_调谐器\_频率**](ksproperty-bda-rf-tuner-frequency.md)  
通知信号承运人的基频率调谐器节点。 基频率乘以值 KSPROPERTY\_BDA\_RF\_调谐器\_频率\_乘数属性来获取实际的频率。

<span id="KSPROPERTY_BDA_RF_TUNER_POLARITY"></span><span id="ksproperty_bda_rf_tuner_polarity"></span>[**KSPROPERTY\_BDA\_RF\_调谐器\_极性**](ksproperty-bda-rf-tuner-polarity.md)  
有关使用传输信号极化通知调谐器节点。

<span id="KSPROPERTY_BDA_RF_TUNER_RANGE"></span><span id="ksproperty_bda_rf_tuner_range"></span>[**KSPROPERTY\_BDA\_RF\_调谐器\_范围**](ksproperty-bda-rf-tuner-range.md)  
调谐器范围设置。

<span id="KSPROPERTY_BDA_RF_TUNER_TRANSPONDER"></span><span id="ksproperty_bda_rf_tuner_transponder"></span>[**KSPROPERTY\_BDA\_RF\_调谐器\_转发器**](ksproperty-bda-rf-tuner-transponder.md)  
通知适当的转发器数量的调谐器节点。

<span id="KSPROPERTY_BDA_RF_TUNER_BANDWIDTH"></span><span id="ksproperty_bda_rf_tuner_bandwidth"></span>[**KSPROPERTY\_BDA\_RF\_调谐器\_带宽**](ksproperty-bda-rf-tuner-bandwidth.md)  
通知的带宽传输信号的调谐器节点。

<span id="KSPROPERTY_BDA_RF_TUNER_FREQUENCY_MULTIPLIER"></span><span id="ksproperty_bda_rf_tuner_frequency_multiplier"></span>[**KSPROPERTY\_BDA\_RF\_调谐器\_频率\_乘数**](ksproperty-bda-rf-tuner-frequency-multiplier.md)  
用来与 KSPROPERTY 值相乘的值会告知调谐器节点\_BDA\_RF\_调谐器\_频率属性来获取实际的频率。

### <a name="comments"></a>备注

KSPROPSETID\_BdaFrequencyFilter 属性集是泛型的在几乎所有的调谐器。 它用来通知如何优化 RF 信号的调谐器节点。

 

 





