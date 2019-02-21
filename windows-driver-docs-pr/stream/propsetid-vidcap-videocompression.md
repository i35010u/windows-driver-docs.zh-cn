---
title: PROPSETID\_VIDCAP\_VIDEOCOMPRESSION
description: PROPSETID\_VIDCAP\_VIDEOCOMPRESSION
ms.assetid: 7af6f7f0-d446-4b44-9423-efd37f731e0b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70c4b7bea33a0f37fe006bd7e4fea498966d13b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519072"
---
# <a name="propsetidvidcapvideocompression"></a>PROPSETID\_VIDCAP\_VIDEOCOMPRESSION


## <span id="ddk_propsetid_vidcap_videocompression_ks"></span><span id="DDK_PROPSETID_VIDCAP_VIDEOCOMPRESSION_KS"></span>


PROPSETID\_VIDCAP\_VIDEOCOMPRESSION 属性设置控制设备的视频的压缩设置。

KSPROPERTY\_VIDCAP\_中的 VIDEOCOMPRESSION 枚举*ksmedia.h*指定此集的属性。

支持设置此属性是可选的应仅通过实现将视频的压缩编解码器的设备来实现。

视频捕获微型驱动程序需要实现以下属性：

[**KSPROPERTY\_VIDEOCOMPRESSION\_GETINFO**](ksproperty-videocompression-getinfo.md)

[**KSPROPERTY\_VIDEOCOMPRESSION\_KEYFRAME\_RATE**](ksproperty-videocompression-keyframe-rate.md)

[**KSPROPERTY\_VIDEOCOMPRESSION\_重写\_帧\_大小**](ksproperty-videocompression-override-frame-size.md)

[**KSPROPERTY\_VIDEOCOMPRESSION\_OVERRIDE\_KEYFRAME**](ksproperty-videocompression-override-keyframe.md)

[**KSPROPERTY\_VIDEOCOMPRESSION\_PFRAMES\_每\_关键帧**](ksproperty-videocompression-pframes-per-keyframe.md)

[**KSPROPERTY\_VIDEOCOMPRESSION\_质量**](ksproperty-videocompression-quality.md)

[**KSPROPERTY\_VIDEOCOMPRESSION\_窗口大小**](ksproperty-videocompression-windowsize.md)

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow 接口

DirectShow **IAMVideoCompression**接口 （请参阅 Microsoft Windows SDK 中的 DirectShow 文档） 提供对此集的属性的访问。

 

 





