---
title: PROPSETID \_ VIDCAP \_ VIDEOCOMPRESSION
description: PROPSETID \_ VIDCAP \_ VIDEOCOMPRESSION
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d23f55defd7966dac99bbf8ed6a351d3888ded1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840507"
---
# <a name="propsetid_vidcap_videocompression"></a>PROPSETID \_ VIDCAP \_ VIDEOCOMPRESSION


## <span id="ddk_propsetid_vidcap_videocompression_ks"></span><span id="DDK_PROPSETID_VIDCAP_VIDEOCOMPRESSION_KS"></span>


PROPSETID \_ VIDCAP \_ VIDEOCOMPRESSION 属性集控制设备的视频压缩设置。

\_Ksmedia 中的 KSPROPERTY VIDCAP \_ VIDEOCOMPRESSION *ksmedia.h* 枚举指定此集的属性。

对此属性集的支持是可选的，只应由实现视频压缩编解码器的设备来实现。

需要视频捕获微型驱动程序来实现以下属性：

[**KSPROPERTY \_ VIDEOCOMPRESSION \_ GETINFO**](ksproperty-videocompression-getinfo.md)

[**KSPROPERTY \_ VIDEOCOMPRESSION \_ 关键帧 \_ 速率**](ksproperty-videocompression-keyframe-rate.md)

[**KSPROPERTY \_ VIDEOCOMPRESSION \_ 替代 \_ 帧 \_ 大小**](ksproperty-videocompression-override-frame-size.md)

[**KSPROPERTY \_ VIDEOCOMPRESSION \_ 替代 \_ 关键帧**](ksproperty-videocompression-override-keyframe.md)

[**\_ \_ \_ 每个 \_ 关键帧的 KSPROPERTY VIDEOCOMPRESSION PFRAMES**](ksproperty-videocompression-pframes-per-keyframe.md)

[**KSPROPERTY \_ VIDEOCOMPRESSION \_ QUALITY**](ksproperty-videocompression-quality.md)

[**KSPROPERTY \_ VIDEOCOMPRESSION \_ WINDOWSIZE**](ksproperty-videocompression-windowsize.md)

### <a name="span-iddirectshow_interfacespanspan-iddirectshow_interfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow 接口

DirectShow **IAMVideoCompression** 接口 (参阅 Microsoft Windows SDK 中的 directshow 文档) 提供对此集的属性的访问权限。

 

 





