---
title: KSNODETYPE\_PROLOGIC\_解码器
description: KSNODETYPE\_PROLOGIC\_解码器
ms.assetid: 905ff503-1aff-4490-bd6f-f6bec8e7c3d6
keywords:
- KSNODETYPE_PROLOGIC_DECODER 音频设备
topic_type:
- apiref
api_name:
- KSNODETYPE_PROLOGIC_DECODER
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1cdc6aeb7e0627fea33da6e160b49b75c596c5c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333198"
---
# <a name="ksnodetypeprologicdecoder"></a>KSNODETYPE\_PROLOGIC\_解码器


## <span id="ddk_ksnodetype_prologic_decoder_ks"></span><span id="DDK_KSNODETYPE_PROLOGIC_DECODER_KS"></span>


KSNODETYPE\_PROLOGIC\_解码器节点表示 Dolby Surround Pro 逻辑解码器。 该解码器控件具有一个立体声输入的流和一至四个频道的一个输出流。 4 个通道输出格式，通道被映射到左、 右、 中心和后演讲者。 在三个通道输出格式中，通道映射到 left、 right 和扬声器。

功能 KSNODETYPE\_PROLOGIC\_解码器节点是补充[ **KSNODETYPE\_PROLOGIC\_编码器**](ksnodetype-prologic-encoder.md)节点，它将四个通道的输入的流转换为环绕声编码的立体声输出流。

KSNODETYPE\_PROLOGIC\_解码器节点应支持以下必需的属性：

[**KSPROPERTY\_音频\_通道\_配置**](ksproperty-audio-channel-config.md)

[**KSPROPERTY\_TOPOLOGYNODE\_启用**](ksproperty-topologynode-enable.md)

[**KSPROPERTY\_TOPOLOGYNODE\_重置**](ksproperty-topologynode-reset.md)

KSPROPERTY\_音频\_通道\_配置属性设置，并获取该节点的输出流的通道配置。

 

 





