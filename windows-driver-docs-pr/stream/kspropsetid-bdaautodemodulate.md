---
title: KSPROPSETID \_ BdaAutodemodulate
description: KSPROPSETID \_ BdaAutodemodulate
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9016fc07ad7cd00000427fc4432c4a2829cc4dd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786613"
---
# <a name="kspropsetid_bdaautodemodulate"></a>KSPROPSETID \_ BdaAutodemodulate


## <span id="ddk_kspropsetid_bdaautodemodulate_ks"></span><span id="DDK_KSPROPSETID_BDAAUTODEMODULATE_KS"></span>


KSPROPSETID \_ BdaAutodemodulate 为 BDA autodemodulate 属性集。 它用于控制可自动确定调制信号和 demodulate 的特征的信号解调器节点。

以下属性可用：

<span id="KSPROPERTY_BDA_AUTODEMODULATE_START"></span><span id="ksproperty_bda_autodemodulate_start"></span>[**KSPROPERTY \_ BDA \_ AUTODEMODULATE \_ START**](ksproperty-bda-autodemodulate-start.md)  
当某个解调器节点处于暂停或运行状态时，它会尝试自动确定调制参数，并 demodulate 信号。

<span id="KSPROPERTY_BDA_AUTODEMODULATE_STOP"></span><span id="ksproperty_bda_autodemodulate_stop"></span>[**KSPROPERTY \_ BDA \_ AUTODEMODULATE \_ STOP**](ksproperty-bda-autodemodulate-stop.md)  
通知解调器节点应停止尝试自动 demodulate 信号。

### <a name="comments"></a>注释

KSPROPSETID \_ BdaAutodemodulate 还用于解调器节点，例如仅支持调制参数的一项配置的8VSB 解调器节点。 对于这两种类型的节点，不会通知该解调器设置特定值，如内部和外部正向纠错 (FEC) 方法。

 

 





