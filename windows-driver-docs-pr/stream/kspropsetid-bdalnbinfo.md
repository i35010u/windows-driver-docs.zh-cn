---
title: KSPROPSETID \_ BdaLNBInfo
description: KSPROPSETID \_ BdaLNBInfo
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 555e463d7f095ad418f7e5b3e4c6ff9b0bdddf11
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792091"
---
# <a name="kspropsetid_bdalnbinfo"></a>KSPROPSETID \_ BdaLNBInfo


## <span id="ddk_kspropsetid_bdalnbinfo_ks"></span><span id="DDK_KSPROPSETID_BDALNBINFO_KS"></span>


KSPROPSETID \_ BdaLNBInfo 是 (LNB) 信息属性集的 BDA 低噪音块。 它用于向 RF 调谐器提供有关附属 dish 的 LNB 设备的信息。

以下属性可用：

<span id="KSPROPERTY_BDA_LNB_LOF_LOW_BAND"></span><span id="ksproperty_bda_lnb_lof_low_band"></span>[**KSPROPERTY \_ BDA \_ LNB \_ LOF \_ LOW \_**](ksproperty-bda-lnb-lof-low-band.md)  
通知 RF 调谐器节点 (LOF) ，该频率由 LNB 用于改变传入的低压 RF 信号的频率。

<span id="KSPROPERTY_BDA_LNB_LOF_HIGH_BAND"></span><span id="ksproperty_bda_lnb_lof_high_band"></span>[**KSPROPERTY \_ BDA \_ LNB \_ LOF \_ 高层 \_**](ksproperty-bda-lnb-lof-high-band.md)  
向 RF 调谐器节点通知 LNB 使用的 LOF，以改变传入的带外 RF 信号的频率。

<span id="KSPROPERTY_BDA_LNB_SWITCH_FREQUENCY"></span><span id="ksproperty_bda_lnb_switch_frequency"></span>[**KSPROPERTY \_ BDA \_ LNB \_ 交换机 \_ 频率**](ksproperty-bda-lnb-switch-frequency.md)  
通知 RF 调谐器节点有关传入 RF 信号的频率，调谐器应通知 LNB 设备使用带外 lof 来使用带外 LOF，反之亦然。

### <a name="comments"></a>注释

LNB 是卫星 dish 的焦点设备。 LNB 收集由 dish 反射的信号，并将其发送到 RF 调谐器的 LNB 放大器。

KSPROPSETID \_ BdaLNBInfo 属性集将有关附属 dish 的 LNB 设备的信息传递给 RF 调谐器。 当客户端发送 [**KSPROPERTY \_ BDA \_ rf \_ \_**](ksproperty-bda-rf-tuner-frequency.md) 射频请求以将 RF 调谐器调整到特定频率时，调谐器可以发送（如果需要），将信号控制到 LNB 设备，根据 LNB 的属性调整内部参数。

### <a name="see-also"></a>另请参阅

[**KSPROPERTY \_ BDA \_ RF \_ 调谐器 \_ 频率**](ksproperty-bda-rf-tuner-frequency.md)

 

 





