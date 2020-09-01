---
title: KSNODETYPE \_ 卷
description: KSNODETYPE \_ 卷
ms.assetid: 4776ea69-6492-428e-97ce-dd8842f22c16
keywords:
- KSNODETYPE_VOLUME 音频设备
topic_type:
- apiref
api_name:
- KSNODETYPE_VOLUME
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73855533ca2a5c9ede99c774f2a7dcc731759fcd
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206997"
---
# <a name="ksnodetype_volume"></a>KSNODETYPE \_ 卷


## <span id="ddk_ksnodetype_volume_ks"></span><span id="DDK_KSNODETYPE_VOLUME_KS"></span>


KSNODETYPE \_ 卷节点表示) 控制 (增益或衰减量。 卷控件有一个输入流和一个输出流;这两个流中的每一个都具有相同的数据格式。 它可以在卷) 中应用衰减 (降低，或提高 (卷) 增加到流的数量。 此外，它还可以选择支持反应反的信号。

有关多通道卷节点的信息，请参阅 [公开多通道节点](./exposing-multichannel-nodes.md)。

KSNODETYPE \_ 卷节点应支持以下必需属性：

[**KSPROPERTY \_ 音频 \_ VOLUMELEVEL**](ksproperty-audio-volumelevel.md)

 

