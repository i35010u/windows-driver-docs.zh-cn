---
title: PROPSETID\_VIDCAP\_VIDEODECODER
description: PROPSETID\_VIDCAP\_VIDEODECODER
ms.assetid: 86b581b7-51fd-4662-8291-4c5baf9d3b16
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97b413a1eac496ff8ab05518b6570cb941f2788f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519109"
---
# <a name="propsetidvidcapvideodecoder"></a>PROPSETID\_VIDCAP\_VIDEODECODER


## <span id="ddk_propsetid_vidcap_videodecoder_ks"></span><span id="DDK_PROPSETID_VIDCAP_VIDEODECODER_KS"></span>


PROPSETID\_VIDCAP\_VIDEODECODER 属性设置控制模拟视频解码器的设备。 模拟的视频解码器转换为数字格式如 RGB 或 YUV 基带模拟视频信号。

KSPROPERTY\_VIDCAP\_中的 VIDEODECODER 枚举*ksmedia.h*指定此集的属性。

支持设置此属性是可选的应仅通过模拟视频捕获设备来实现。

视频捕获微型驱动程序需要实现以下属性：

[**KSPROPERTY\_VIDEODECODER\_CAP**](ksproperty-videodecoder-caps.md)

[**KSPROPERTY\_VIDEODECODER\_标准**](ksproperty-videodecoder-standard.md)

[**KSPROPERTY\_VIDEODECODER\_状态**](ksproperty-videodecoder-status.md)

视频捕获微型驱动程序可以根据需要实现以下属性：

[**KSPROPERTY\_VIDEODECODER\_输出\_启用**](ksproperty-videodecoder-output-enable.md)

[**KSPROPERTY\_VIDEODECODER\_VCR\_TIMING**](ksproperty-videodecoder-vcr-timing.md)

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow 接口

DirectShow **IAMAnalogVideoDecoder**接口 （请参阅 Microsoft Windows SDK 中的 DirectShow 文档） 提供对此集的属性的访问。

 

 





