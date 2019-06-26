---
title: KSNODETYPE\_卷
description: KSNODETYPE\_卷
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
ms.openlocfilehash: feb4a582311c86625216a380c198a6d0915d7d75
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359008"
---
# <a name="ksnodetypevolume"></a>KSNODETYPE\_卷


## <span id="ddk_ksnodetype_volume_ks"></span><span id="DDK_KSNODETYPE_VOLUME_KS"></span>


KSNODETYPE\_卷节点表示的卷 （收益或衰减） 控件。 卷在控件有一个输入的流和一个输出流;两个流的每个具有相同的数据格式。 它可以应用衰减 （种数量缩减） 或提升 （增加卷） 到流。 此外，可以选择性地支持反转信号。

有关多渠道卷节点的信息，请参阅[公开多通道节点](https://docs.microsoft.com/windows-hardware/drivers/audio/exposing-multichannel-nodes)。

KSNODETYPE\_卷节点应支持以下必需的属性：

[**KSPROPERTY\_音频\_VOLUMELEVEL**](ksproperty-audio-volumelevel.md)

 

 





