---
title: KSNODETYPE \_ PROLOGIC \_ 编码器
description: KSNODETYPE \_ PROLOGIC \_ 编码器
keywords:
- KSNODETYPE_PROLOGIC_ENCODER 音频设备
topic_type:
- apiref
api_name:
- KSNODETYPE_PROLOGIC_ENCODER
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcb8102184421ea4affae6da48d57e711102fc69
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799133"
---
# <a name="ksnodetype_prologic_encoder"></a>KSNODETYPE \_ PROLOGIC \_ 编码器


## <span id="ddk_ksnodetype_prologic_encoder_ks"></span><span id="DDK_KSNODETYPE_PROLOGIC_ENCODER_KS"></span>


KSNODETYPE \_ PROLOGIC \_ 编码器节点表示杜比环绕 Pro 逻辑编码器。 节点接受带有通道的四通道输入流，用于左、右、下和后扬声器。 节点将输入流编码为环绕音编码的立体声输出流。

KSNODETYPE \_ PROLOGIC 编码器节点的功能 \_ 是对 [**KSNODETYPE \_ PROLOGIC \_ 解码器**](ksnodetype-prologic-decoder.md) 节点的补充，该节点采用环绕式立体声输入流，并将其解码为包含左、右、中和后扬声器通道的四通道流。

在 Microsoft Windows XP 和更高版本中， [KMixer 系统驱动程序](./kernel-mode-wdm-audio-components.md#kmixer-system-driver) 具有 KSNODETYPE \_ PROLOGIC \_ 编码器节点。

KSNODETYPE \_ PROLOGIC \_ 编码器节点应支持 [**KSPROPERTY \_ 音频 \_ 环绕 \_ 编码**](ksproperty-audio-surround-encode.md) 属性，该属性用于启用和禁用节点。

 

