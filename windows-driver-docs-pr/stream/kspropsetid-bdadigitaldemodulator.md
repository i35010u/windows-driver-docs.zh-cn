---
title: KSPROPSETID\_BdaDigitalDemodulator
description: KSPROPSETID\_BdaDigitalDemodulator
ms.assetid: 536c247d-049b-4d48-96b7-f2aa01f1fa91
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab3c5945c68444e0134f383640a330368b52276f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522487"
---
# <a name="kspropsetidbdadigitaldemodulator"></a>KSPROPSETID\_BdaDigitalDemodulator


## <span id="ddk_kspropsetid_bdadigitaldemodulator_ks"></span><span id="DDK_KSPROPSETID_BDADIGITALDEMODULATOR_KS"></span>


KSPROPSETID\_BdaDigitalDemodulator 是 BDA 数字解调器属性集。 它用于控制需要要设置特定值的信号解调器节点。

可用属性如下：

<span id="KSPROPERTY_BDA_MODULATION_TYPE"></span><span id="ksproperty_bda_modulation_type"></span>[**KSPROPERTY\_BDA\_MODULATION\_TYPE**](ksproperty-bda-modulation-type.md)  
设置或检索解调器类型，例如 QPSK 或 8VSB。

<span id="KSPROPERTY_BDA_INNER_FEC_TYPE"></span><span id="ksproperty_bda_inner_fec_type"></span>[**KSPROPERTY\_BDA\_内部\_FEC\_类型**](ksproperty-bda-inner-fec-type.md)  
设置或检索内部转发错误纠错 (FEC) 类型。

<span id="KSPROPERTY_BDA_INNER_FEC_RATE"></span><span id="ksproperty_bda_inner_fec_rate"></span>[**KSPROPERTY\_BDA\_内部\_FEC\_速率**](ksproperty-bda-inner-fec-rate.md)  
设置或检索用于内部 FEC.的二进制卷积方案

<span id="KSPROPERTY_BDA_OUTER_FEC_TYPE"></span><span id="ksproperty_bda_outer_fec_type"></span>[**KSPROPERTY\_BDA\_OUTER\_FEC\_类型**](ksproperty-bda-outer-fec-type.md)  
设置或检索外部 FEC 类型。

<span id="KSPROPERTY_BDA_OUTER_FEC_RATE"></span><span id="ksproperty_bda_outer_fec_rate"></span>[**KSPROPERTY\_BDA\_OUTER\_FEC\_速率**](ksproperty-bda-outer-fec-rate.md)  
设置或检索二进制卷积编码用于外部 FEC.方案

<span id="KSPROPERTY_BDA_SYMBOL_RATE"></span><span id="ksproperty_bda_symbol_rate"></span>[**KSPROPERTY\_BDA\_SYMBOL\_RATE**](ksproperty-bda-symbol-rate.md)  
设置或检索的符号速率。

<span id="KSPROPERTY_BDA_SPECTRAL_INVERSION"></span><span id="ksproperty_bda_spectral_inversion"></span>[**KSPROPERTY\_BDA\_SPECTRAL\_INVERSION**](ksproperty-bda-spectral-inversion.md)  
设置或检索光谱反转的设置。

<span id="KSPROPERTY_BDA_GUARD_INTERVAL"></span><span id="ksproperty_bda_guard_interval"></span>[**KSPROPERTY\_BDA\_GUARD\_INTERVAL**](ksproperty-bda-guard-interval.md)  
设置或检索防护间隔的设置。

<span id="KSPROPERTY_BDA_TRANSMISSION_MODE"></span><span id="ksproperty_bda_transmission_mode"></span>[**KSPROPERTY\_BDA\_传输\_模式**](ksproperty-bda-transmission-mode.md)  
设置或检索有关如何广播信号进行传输的设置。

### <a name="comments"></a>备注

KSPROPSETID\_BdaDigitalDemodulator 属性集介绍 DVB 解调器节点的属性。 使用此属性集，而不是 KSPROPSETID\_BdaAutodemodulate 如果解调器要求要设置特定值。

### <a name="see-also"></a>另请参阅

[KSPROPSETID\_BdaAutodemodulate](kspropsetid-bdaautodemodulate.md)

 

 





