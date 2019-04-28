---
title: KSNODETYPE\_均衡器
description: KSNODETYPE\_均衡器
ms.assetid: 03812936-57ba-4762-b716-858b7f14908f
keywords:
- KSNODETYPE_EQUALIZER 音频设备
topic_type:
- apiref
api_name:
- KSNODETYPE_EQUALIZER
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 566c2d5eb58377f0c39a5afa2a789c97b74ed044
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333206"
---
# <a name="ksnodetypeequalizer"></a>KSNODETYPE\_均衡器


## <span id="ddk_ksnodetype_equalizer_ks"></span><span id="DDK_KSNODETYPE_EQUALIZER_KS"></span>


KSNODETYPE\_均衡器节点表示具有多个频率带区均衡器。 通过调整均衡表将分配给每个频率带区的级别，EQ 节点可以控制每个节点的输出流中出现的频率带区的量。

EQ 节点具有一个输入的流和一个输出流，并在两个流共享通用的数据格式。

KSNODETYPE\_均衡器节点应支持以下必需的属性：

[**KSPROPERTY\_AUDIO\_EQ\_LEVEL**](ksproperty-audio-eq-level.md)

[**KSPROPERTY\_AUDIO\_NUM\_EQ\_BANDS**](ksproperty-audio-num-eq-bands.md)

[**KSPROPERTY\_AUDIO\_EQ\_BANDS**](ksproperty-audio-eq-bands.md)

 

 





