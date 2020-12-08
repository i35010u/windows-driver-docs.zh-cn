---
title: KSPROPSETID \_ BdaDigitalDemodulator
description: KSPROPSETID \_ BdaDigitalDemodulator
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86e35dcc04dac121306cf06448a1067de83852ae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806639"
---
# <a name="kspropsetid_bdadigitaldemodulator"></a>KSPROPSETID \_ BdaDigitalDemodulator


## <span id="ddk_kspropsetid_bdadigitaldemodulator_ks"></span><span id="DDK_KSPROPSETID_BDADIGITALDEMODULATOR_KS"></span>


KSPROPSETID \_ BdaDigitalDemodulator 是 BDA 数字解调器属性集。 它用于控制需要设置特定值的信号解调器节点。

以下属性可用：

<span id="KSPROPERTY_BDA_MODULATION_TYPE"></span><span id="ksproperty_bda_modulation_type"></span>[**KSPROPERTY \_ BDA \_ 调制 \_ 类型**](ksproperty-bda-modulation-type.md)  
设置或检索解调器类型，如 QPSK 或8VSB。

<span id="KSPROPERTY_BDA_INNER_FEC_TYPE"></span><span id="ksproperty_bda_inner_fec_type"></span>[**KSPROPERTY \_ BDA \_ 内 \_ FEC \_ 类型**](ksproperty-bda-inner-fec-type.md)  
设置或检索 FEC) 类型的内部正向错误 (更正。

<span id="KSPROPERTY_BDA_INNER_FEC_RATE"></span><span id="ksproperty_bda_inner_fec_rate"></span>[**KSPROPERTY \_ BDA \_ 内 \_ FEC \_ 速率**](ksproperty-bda-inner-fec-rate.md)  
设置或检索用于内部 FEC 的二进制卷积方案。

<span id="KSPROPERTY_BDA_OUTER_FEC_TYPE"></span><span id="ksproperty_bda_outer_fec_type"></span>[**KSPROPERTY \_ BDA \_ OUTER \_ FEC \_ 类型**](ksproperty-bda-outer-fec-type.md)  
设置或检索外部 FEC 类型。

<span id="KSPROPERTY_BDA_OUTER_FEC_RATE"></span><span id="ksproperty_bda_outer_fec_rate"></span>[**KSPROPERTY \_ BDA \_ OUTER \_ FEC \_ RATE**](ksproperty-bda-outer-fec-rate.md)  
设置或检索用于外部 FEC 的二进制卷积编码方案。

<span id="KSPROPERTY_BDA_SYMBOL_RATE"></span><span id="ksproperty_bda_symbol_rate"></span>[**KSPROPERTY \_ BDA \_ 符号 \_ 速率**](ksproperty-bda-symbol-rate.md)  
设置或检索符号速率。

<span id="KSPROPERTY_BDA_SPECTRAL_INVERSION"></span><span id="ksproperty_bda_spectral_inversion"></span>[**KSPROPERTY \_ BDA \_ SPECTRAL \_ 反转**](ksproperty-bda-spectral-inversion.md)  
设置或检索 spectral 反转的设置。

<span id="KSPROPERTY_BDA_GUARD_INTERVAL"></span><span id="ksproperty_bda_guard_interval"></span>[**KSPROPERTY \_ BDA \_ GUARD \_ 间隔**](ksproperty-bda-guard-interval.md)  
设置或检索临界间隔的设置。

<span id="KSPROPERTY_BDA_TRANSMISSION_MODE"></span><span id="ksproperty_bda_transmission_mode"></span>[**KSPROPERTY \_ BDA \_ 传输 \_ 模式**](ksproperty-bda-transmission-mode.md)  
设置或检索如何传输广播信号的设置。

### <a name="comments"></a>注释

KSPROPSETID \_ BdaDigitalDemodulator 属性集描述了 DVB 解调器节点的属性。 如果需要设置特定值，请使用此属性集而不是 KSPROPSETID \_ BdaAutodemodulate。

### <a name="see-also"></a>另请参阅

[KSPROPSETID \_ BdaAutodemodulate](kspropsetid-bdaautodemodulate.md)

 

 





