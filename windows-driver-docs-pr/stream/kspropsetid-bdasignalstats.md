---
title: KSPROPSETID \_ BdaSignalStats
description: KSPROPSETID \_ BdaSignalStats
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1fe5d76abe742ba0f4dea8d4484c40437143c9a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809863"
---
# <a name="kspropsetid_bdasignalstats"></a>KSPROPSETID \_ BdaSignalStats


## <span id="ddk_kspropsetid_bdasignalstats_ks"></span><span id="DDK_KSPROPSETID_BDASIGNALSTATS_KS"></span>


KSPROPSETID \_ BdaSignalStats 为 "BDA 信号统计信息" 属性集。 它用于从控制节点或 pin 检索信号统计信息。

以下属性可用：

<span id="KSPROPERTY_BDA_SIGNAL_STRENGTH"></span><span id="ksproperty_bda_signal_strength"></span>[**KSPROPERTY \_需要 BDA \_ 信号 \_ 强度**](ksproperty-bda-signal-strength.md) 。
指示 (DB) 的 DB 中，mDb (1/1000 的载波强度。
<span id="KSPROPERTY_BDA_SIGNAL_QUALITY"></span><span id="ksproperty_bda_signal_quality"></span>[**KSPROPERTY \_需要 BDA \_ 信号 \_ 质量**](ksproperty-bda-signal-quality.md) 。
指示以百分比形式从信号中成功提取的数据量。
<span id="KSPROPERTY_BDA_SIGNAL_PRESENT"></span><span id="ksproperty_bda_signal_present"></span>[**KSPROPERTY \_需要 \_ \_ 提供 BDA 信号**](ksproperty-bda-signal-present.md) 。
指示是否存在信号载波。
<span id="KSPROPERTY_BDA_SIGNAL_LOCKED"></span><span id="ksproperty_bda_signal_locked"></span>[**KSPROPERTY \_需要 \_ \_ 锁定 BDA 信号**](ksproperty-bda-signal-locked.md) 。
指示是否可以锁定信号。
<span id="KSPROPERTY_BDA_SAMPLE_TIME"></span><span id="ksproperty_bda_sample_time"></span>[**KSPROPERTY \_BDA \_ 示例 \_ 时间**](ksproperty-bda-sample-time.md) 为可选。
指示用于计算信号级别和质量的采样时间。
<span id="KSPROPERTY_BDA_SIGNAL_LOCK_CAPS"></span><span id="ksproperty_bda_signal_lock_caps"></span>[**KSPROPERTY \_需要 BDA \_ 信号 \_ 锁定 \_ 端**](ksproperty-bda-signal-lock-caps.md) 。
指示驱动程序可以为信号支持的锁类型。
<span id="KSPROPERTY_BDA_SIGNAL_LOCK_TYPE"></span><span id="ksproperty_bda_signal_lock_type"></span>[**KSPROPERTY \_需要 BDA \_ 信号 \_ 锁定 \_ 类型**](ksproperty-bda-signal-lock-type.md) 。
指示信号的当前锁类型。
### <a name="comments"></a>注释

当指定 KSPROPSETID \_ BdaSignalStats 属性集的特定属性以从 pin 获取信号统计时，请将 KSP 节点结构 **的** 节点2成员设置 \_ 为−1。

 

 





