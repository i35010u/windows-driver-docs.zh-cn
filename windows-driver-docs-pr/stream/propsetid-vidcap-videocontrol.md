---
title: PROPSETID \_ VIDCAP \_ VIDEOCONTROL
description: PROPSETID \_ VIDCAP \_ VIDEOCONTROL
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f266d200c6ea0a5c2c49ddbe161992aa1909cf6b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840505"
---
# <a name="propsetid_vidcap_videocontrol"></a>PROPSETID \_ VIDCAP \_ VIDEOCONTROL


## <span id="ddk_propsetid_vidcap_videocontrol_ks"></span><span id="DDK_PROPSETID_VIDCAP_VIDEOCONTROL_KS"></span>


PROPOSETID \_ VIDCAP \_ VIDEOCONTROL 属性集控制视频捕获操作的补充方面，如枚举可用帧速率和图像方向。 通常，模拟数字化器可以支持 USB 和1394会议照相机支持的任何帧速率请求，但使用有限的帧速率集。

\_Ksmedia 中的 KSPROPERTY VIDCAP \_ VIDEOCONTROL *ksmedia.h* 枚举指定此集的属性。

对此属性集的支持是可选的，只应由无法以任意帧速率捕获视频的设备微型驱动程序来实现。

需要视频捕获微型驱动程序来实现以下属性：

[**KSPROPERTY \_ VIDEOCONTROL \_ CAP**](ksproperty-videocontrol-caps.md)

视频捕获微型驱动程序可以选择实现以下属性：

[**KSPROPERTY \_ VIDEOCONTROL \_ 实际 \_ 帧 \_ 速率**](ksproperty-videocontrol-actual-frame-rate.md)

[**KSPROPERTY \_ VIDEOCONTROL \_ 帧 \_ 速率**](ksproperty-videocontrol-frame-rates.md)

[**KSPROPERTY \_ VIDEOCONTROL \_ 模式**](ksproperty-videocontrol-mode.md)

### <a name="span-iddirectshow_interfacespanspan-iddirectshow_interfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow 接口

没有可提供对此属性集的访问的 DirectShow 接口。

 

 





