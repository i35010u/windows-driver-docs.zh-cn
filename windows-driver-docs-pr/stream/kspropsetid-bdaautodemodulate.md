---
title: KSPROPSETID\_BdaAutodemodulate
description: KSPROPSETID\_BdaAutodemodulate
ms.assetid: b7c3c934-5b31-48da-9fb0-98007267711b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6ed1fe40e0511e1fcde416be0907067678eef15
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380633"
---
# <a name="kspropsetidbdaautodemodulate"></a>KSPROPSETID\_BdaAutodemodulate


## <span id="ddk_kspropsetid_bdaautodemodulate_ks"></span><span id="DDK_KSPROPSETID_BDAAUTODEMODULATE_KS"></span>


KSPROPSETID\_BdaAutodemodulate 是 BDA autodemodulate 属性集。 它用于控制可自动确定调制的信号的特征和解调信号解调器节点。

可用属性如下：

<span id="KSPROPERTY_BDA_AUTODEMODULATE_START"></span><span id="ksproperty_bda_autodemodulate_start"></span>[**KSPROPERTY\_BDA\_AUTODEMODULATE\_START**](ksproperty-bda-autodemodulate-start.md)  
通知解调器节点，在暂停或运行的状态时，它应尝试自动确定调整参数和解调信号。

<span id="KSPROPERTY_BDA_AUTODEMODULATE_STOP"></span><span id="ksproperty_bda_autodemodulate_stop"></span>[**KSPROPERTY\_BDA\_AUTODEMODULATE\_STOP**](ksproperty-bda-autodemodulate-stop.md)  
它应停止尝试自动解调信号通知解调器节点。

### <a name="comments"></a>备注

KSPROPSETID\_BdaAutodemodulate 还用于解调器节点，例如 8VSB 解调器节点仅支持一个配置的调整参数。 对于这些类型的节点，并没有通知解调器来设置特定值，例如 Inner 和 Outer 前向纠错 (FEC) 方法。

 

 





