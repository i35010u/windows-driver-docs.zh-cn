---
title: KSNODETYPE\_AGC
description: KSNODETYPE\_AGC
ms.assetid: 54d6bb6a-9c15-4020-bc6e-92b24878e1fd
keywords:
- KSNODETYPE_AGC 音频设备
topic_type:
- apiref
api_name:
- KSNODETYPE_AGC
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2676a77bb38cb5aa79a11198112f34d0eb8e47b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566081"
---
# <a name="ksnodetypeagc"></a>KSNODETYPE\_AGC


## <span id="ddk_ksnodetype_agc_ks"></span><span id="DDK_KSNODETYPE_AGC_KS"></span>


KSNODETYPE\_AGC 节点表示自动增益控制 (AGC)。 AGC 节点具有一个输入的流和一个输出流，并在两个流的每个具有相同的数据格式。 节点自动调整衰减或提升应用于输入流，以便实现最大动态范围，而不剪辑信号的量。

KSNODETYPE\_AGC 节点应支持以下属性：

[**KSPROPERTY\_AUDIO\_AGC**](ksproperty-audio-agc.md)

KSNODETYPE\_AGC 节点还可以支持以下可选属性：

[**KSPROPERTY\_TOPOLOGYNODE\_启用**](ksproperty-topologynode-enable.md)

[**KSPROPERTY\_TOPOLOGYNODE\_重置**](ksproperty-topologynode-reset.md)

KSPROPERTY\_TOPOLOGYNODE\_启用属性用于同时启用和禁用节点。 该节点禁用时，在直通模式下运行 （也就是说，它允许要传递到无需修改输出的输入的流）。

 

 





