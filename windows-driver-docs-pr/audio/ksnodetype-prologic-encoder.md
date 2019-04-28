---
title: KSNODETYPE\_PROLOGIC\_编码器
description: KSNODETYPE\_PROLOGIC\_编码器
ms.assetid: cca6fe1d-20f8-4112-956b-a1b33b48a4ff
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
ms.openlocfilehash: 15a60a784484c5d112d0a6aa580f79a1061b2aa4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333222"
---
# <a name="ksnodetypeprologicencoder"></a>KSNODETYPE\_PROLOGIC\_编码器


## <span id="ddk_ksnodetype_prologic_encoder_ks"></span><span id="DDK_KSNODETYPE_PROLOGIC_ENCODER_KS"></span>


KSNODETYPE\_PROLOGIC\_编码器节点表示 Dolby Surround Pro 逻辑编码器。 节点接受通道左侧、 右侧、 中心和后置扬声器的 4 个通道输入的流。 该节点将输入的流编码为环绕声编码的立体声输出流。

功能 KSNODETYPE\_PROLOGIC\_编码器节点是补充[ **KSNODETYPE\_PROLOGIC\_解码器**](ksnodetype-prologic-decoder.md)节点，这采用的环绕声编码的立体声输入的流，并将其解码到 4 个通道流的左侧、 右侧、 中心和后置扬声器的频道。

在 Microsoft Windows XP 及更高版本， [KMixer 系统驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff537039#kmixer-system-driver)具有 KSNODETYPE\_PROLOGIC\_编码器节点。

KSNODETYPE\_PROLOGIC\_编码器节点应支持[ **KSPROPERTY\_音频\_环绕\_编码**](ksproperty-audio-surround-encode.md)属性，用于启用和禁用节点。

 

 





