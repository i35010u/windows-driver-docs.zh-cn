---
title: KSPROPSETID\_BdaSignalStats
description: KSPROPSETID\_BdaSignalStats
ms.assetid: ea368344-e56d-47d1-bc1f-241ba8aa0bc4
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d203b775bb3c4b29e31bd2cf9b7a1168efbfddef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391390"
---
# <a name="kspropsetidbdasignalstats"></a>KSPROPSETID\_BdaSignalStats


## <span id="ddk_kspropsetid_bdasignalstats_ks"></span><span id="DDK_KSPROPSETID_BDASIGNALSTATS_KS"></span>


KSPROPSETID\_BdaSignalStats 是 BDA 信号统计信息属性集。 它用于检索控件节点或 pin 信号统计信息。

可用属性如下：

<span id="KSPROPERTY_BDA_SIGNAL_STRENGTH"></span><span id="ksproperty_bda_signal_strength"></span>[**KSPROPERTY\_BDA\_信号\_强度**](ksproperty-bda-signal-strength.md)所需。
指示在 mDb (1/1000 分贝 (DB)) 中的信号的运营商强度。
<span id="KSPROPERTY_BDA_SIGNAL_QUALITY"></span><span id="ksproperty_bda_signal_quality"></span>[**KSPROPERTY\_BDA\_信号\_质量**](ksproperty-bda-signal-quality.md)所需。
指示已成功从以百分比表示的信号中提取的数据量。
<span id="KSPROPERTY_BDA_SIGNAL_PRESENT"></span><span id="ksproperty_bda_signal_present"></span>[**KSPROPERTY\_BDA\_信号\_存在**](ksproperty-bda-signal-present.md)所需。
指示信号承运人是否存在。
<span id="KSPROPERTY_BDA_SIGNAL_LOCKED"></span><span id="ksproperty_bda_signal_locked"></span>[**KSPROPERTY\_BDA\_信号\_锁定**](ksproperty-bda-signal-locked.md)所需。
指示是否可以锁定信号。
<span id="KSPROPERTY_BDA_SAMPLE_TIME"></span><span id="ksproperty_bda_sample_time"></span>[**KSPROPERTY\_BDA\_示例\_时间**](ksproperty-bda-sample-time.md)可选。
指示通过的信号平均级别和质量的示例时间。
<span id="KSPROPERTY_BDA_SIGNAL_LOCK_CAPS"></span><span id="ksproperty_bda_signal_lock_caps"></span>[**KSPROPERTY\_BDA\_信号\_锁\_CAPS** ](ksproperty-bda-signal-lock-caps.md)所需。
指示该驱动程序可以支持的信号的锁类型。
<span id="KSPROPERTY_BDA_SIGNAL_LOCK_TYPE"></span><span id="ksproperty_bda_signal_lock_type"></span>[**KSPROPERTY\_BDA\_信号\_锁\_类型**](ksproperty-bda-signal-lock-type.md)所需。
指示信号的当前锁类型。
### <a name="comments"></a>备注

当指定的特定属性的 KSPROPSETID\_BdaSignalStats 属性设置为从 pin，获取信号统计信息设置**NodeId**成员的 KSP 的\_到 − 1 的节点结构。

 

 





