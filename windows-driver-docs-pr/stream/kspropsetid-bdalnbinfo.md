---
title: KSPROPSETID\_BdaLNBInfo
description: KSPROPSETID\_BdaLNBInfo
ms.assetid: 2b385e93-2d0d-44ca-9cfc-58afea946db6
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24f1049488fbdeeb88420332f7b8dfdf369b227e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540831"
---
# <a name="kspropsetidbdalnbinfo"></a>KSPROPSETID\_BdaLNBInfo


## <span id="ddk_kspropsetid_bdalnbinfo_ks"></span><span id="DDK_KSPROPSETID_BDALNBINFO_KS"></span>


KSPROPSETID\_BdaLNBInfo 是 BDA 低干扰块 (LNB) 信息属性集。 它用于提供 RF 调谐器卫星电视的 LNB 设备有关的信息。

可用属性如下：

<span id="KSPROPERTY_BDA_LNB_LOF_LOW_BAND"></span><span id="ksproperty_bda_lnb_lof_low_band"></span>[**KSPROPERTY\_BDA\_LNB\_LOF\_LOW\_BAND**](ksproperty-bda-lnb-lof-low-band.md)  
通知由 LNB 转换传入低外 RF 信号的频率的本地震荡频率 (LOF) RF 调谐器节点。

<span id="KSPROPERTY_BDA_LNB_LOF_HIGH_BAND"></span><span id="ksproperty_bda_lnb_lof_high_band"></span>[**KSPROPERTY\_BDA\_LNB\_LOF\_高\_外**](ksproperty-bda-lnb-lof-high-band.md)  
通知转换传入高外 RF 信号的频率由 LNB LOF RF 调谐器节点。

<span id="KSPROPERTY_BDA_LNB_SWITCH_FREQUENCY"></span><span id="ksproperty_bda_lnb_switch_frequency"></span>[**KSPROPERTY\_BDA\_LNB\_SWITCH\_FREQUENCY**](ksproperty-bda-lnb-switch-frequency.md)  
RF 调谐器节点告知传入 RF 信号的调谐器应该通知 LNB 设备可以从使用低外的 LOF 使用高外 LOF，反之亦然切换的频率。

### <a name="comments"></a>备注

LNB 是设备所带来的卫星电视的焦点。 LNB 收集反映的电视信号，并将其发送到 RF 调谐器 LNB 放大器。

KSPROPSETID\_BdaLNBInfo 属性集通信到 RF 调谐器的卫星电视的 LNB 设备的相关信息。 当客户端发送[ **KSPROPERTY\_BDA\_RF\_调谐器\_频率**](ksproperty-bda-rf-tuner-frequency.md)请求来优化该调谐器可以发送到特定的频率，RF 调谐器如果需要，控制到 LNB 设备的信号以调整根据 LNB 属性的内部参数。

### <a name="see-also"></a>另请参阅

[**KSPROPERTY\_BDA\_RF\_调谐器\_频率**](ksproperty-bda-rf-tuner-frequency.md)

 

 





