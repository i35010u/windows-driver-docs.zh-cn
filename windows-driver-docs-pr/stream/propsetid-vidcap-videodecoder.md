---
title: PROPSETID \_ VIDCAP \_ VIDEODECODER
description: PROPSETID \_ VIDCAP \_ VIDEODECODER
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82d243dddd588b2a145d8ad43ae482e2b0eb31bb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818757"
---
# <a name="propsetid_vidcap_videodecoder"></a>PROPSETID \_ VIDCAP \_ VIDEODECODER


## <span id="ddk_propsetid_vidcap_videodecoder_ks"></span><span id="DDK_PROPSETID_VIDCAP_VIDEODECODER_KS"></span>


PROPSETID \_ VIDCAP \_ VIDEODECODER 属性集控制模拟视频解码器设备。 模拟视频解码器将基带模拟视频信号转换为数字格式，如 RGB 或 YUV。

\_Ksmedia 中的 KSPROPERTY VIDCAP \_ VIDEODECODER *ksmedia.h* 枚举指定此集的属性。

对此属性集的支持是可选的，只应由模拟视频捕获设备实现。

需要视频捕获微型驱动程序来实现以下属性：

[**KSPROPERTY \_ VIDEODECODER \_ CAP**](ksproperty-videodecoder-caps.md)

[**KSPROPERTY \_ VIDEODECODER \_ 标准**](ksproperty-videodecoder-standard.md)

[**KSPROPERTY \_ VIDEODECODER \_ 状态**](ksproperty-videodecoder-status.md)

视频捕获微型驱动程序可以选择实现以下属性：

[**KSPROPERTY \_ VIDEODECODER \_ OUTPUT \_ ENABLE**](ksproperty-videodecoder-output-enable.md)

[**KSPROPERTY \_ VIDEODECODER \_ VCR \_ 计时**](ksproperty-videodecoder-vcr-timing.md)

### <a name="span-iddirectshow_interfacespanspan-iddirectshow_interfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow 接口

DirectShow **IAMAnalogVideoDecoder** 接口 (参阅 Microsoft Windows SDK 中的 directshow 文档) 提供对此集的属性的访问权限。

 

 





