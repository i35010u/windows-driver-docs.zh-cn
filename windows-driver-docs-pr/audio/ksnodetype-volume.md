---
title: KSNODETYPE \_ 卷
description: KSNODETYPE \_ 卷
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
ms.openlocfilehash: c39d58114d5d5989d9b861865e77af9ab4b71bf4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799109"
---
# <a name="ksnodetype_volume"></a>KSNODETYPE \_ 卷


## <span id="ddk_ksnodetype_volume_ks"></span><span id="DDK_KSNODETYPE_VOLUME_KS"></span>


KSNODETYPE \_ 卷节点表示) 控制 (增益或衰减量。 卷控件有一个输入流和一个输出流;这两个流中的每一个都具有相同的数据格式。 它可以在卷) 中应用衰减 (降低，或提高 (卷) 增加到流的数量。 此外，它还可以选择支持反应反的信号。

有关多通道卷节点的信息，请参阅 [公开多通道节点](./exposing-multichannel-nodes.md)。

KSNODETYPE \_ 卷节点应支持以下必需属性：

[**KSPROPERTY \_ 音频 \_ VOLUMELEVEL**](ksproperty-audio-volumelevel.md)

 

