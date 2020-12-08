---
title: KSNODETYPE \_ PROLOGIC \_ 解码器
description: KSNODETYPE \_ PROLOGIC \_ 解码器
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
ms.openlocfilehash: 37a38645efb656a0baa5356de786bd9df1e8bf6f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784613"
---
# <a name="ksnodetype_prologic_decoder"></a>KSNODETYPE \_ PROLOGIC \_ 解码器


## <span id="ddk_ksnodetype_prologic_decoder_ks"></span><span id="DDK_KSNODETYPE_PROLOGIC_DECODER_KS"></span>


KSNODETYPE \_ PROLOGIC \_ 解码器节点表示杜比环绕 Pro 逻辑解码器。 解码器控件具有一个立体声输入流和一个输出流，其中包含一到四个通道。 在四通道输出格式中，通道映射到左、右、中和后扬声器。 在三通道输出格式中，通道映射到左、右和后扬声器。

KSNODETYPE \_ PROLOGIC 解码器节点的功能 \_ 是对 [**KSNODETYPE \_ PROLOGIC \_ 编码器**](ksnodetype-prologic-encoder.md) 节点的补充，该节点将四通道输入流转换为环绕声编码的立体声输出流。

KSNODETYPE \_ PROLOGIC \_ 解码器节点应支持以下必需属性：

[**KSPROPERTY \_ 音频 \_ 通道 \_ 配置**](ksproperty-audio-channel-config.md)

[**KSPROPERTY \_ TOPOLOGYNODE \_ ENABLE**](ksproperty-topologynode-enable.md)

[**KSPROPERTY \_ TOPOLOGYNODE \_ 重置**](ksproperty-topologynode-reset.md)

KSPROPERTY \_ 音频 \_ 通道 \_ CONFIG 属性设置并获取该节点的输出流的通道配置。

 

 





