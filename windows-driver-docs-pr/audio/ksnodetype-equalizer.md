---
title: KSNODETYPE \_ 均衡器
description: KSNODETYPE \_ 均衡器
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
ms.openlocfilehash: 737b6062f4ac2ee26bb64f957ecf7dff695e1bad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784633"
---
# <a name="ksnodetype_equalizer"></a>KSNODETYPE \_ 均衡器


## <span id="ddk_ksnodetype_equalizer_ks"></span><span id="DDK_KSNODETYPE_EQUALIZER_KS"></span>


KSNODETYPE \_ 均衡器节点表示具有多个频率带区的均衡器。 通过调整均衡表分配给每个频率带区的级别，EQ 节点可以控制在节点的输出流中显示的每个频带的量。

EQ 节点有一个输入流和一个输出流，这两个流共享一个通用的数据格式。

KSNODETYPE \_ 均衡器节点应支持以下必需属性：

[**KSPROPERTY \_ 音频 \_ EQ \_ 级别**](ksproperty-audio-eq-level.md)

[**KSPROPERTY \_ 音频 \_ 数字 \_ EQ \_ 带区**](ksproperty-audio-num-eq-bands.md)

[**KSPROPERTY \_ 音频 \_ EQ \_ 带区**](ksproperty-audio-eq-bands.md)

 

 





