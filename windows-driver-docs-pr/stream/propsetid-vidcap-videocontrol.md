---
title: PROPSETID\_VIDCAP\_VIDEOCONTROL
description: PROPSETID\_VIDCAP\_VIDEOCONTROL
ms.assetid: 892663c1-a807-4d03-9af0-f065149e7d42
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bb5c9851e41e63293133c5abdf2e261cf2e5bf4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541086"
---
# <a name="propsetidvidcapvideocontrol"></a>PROPSETID\_VIDCAP\_VIDEOCONTROL


## <span id="ddk_propsetid_vidcap_videocontrol_ks"></span><span id="DDK_PROPSETID_VIDCAP_VIDEOCONTROL_KS"></span>


PROPOSETID\_VIDCAP\_VIDEOCONTROL 属性设置控件的视频捕获操作，例如枚举可用的帧速率和图像方向的补充方面。 通常情况下，模拟数字化器可以支持任何 USB 和 1394年会议摄像机支持，但具有有限的帧速率的帧速率请求。

KSPROPERTY\_VIDCAP\_中的 VIDEOCONTROL 枚举*ksmedia.h*指定此集的属性。

支持设置此属性是可选的应仅由微型驱动程序不能捕获在任意帧速率视频的设备的实现。

视频捕获微型驱动程序需要实现以下属性：

[**KSPROPERTY\_VIDEOCONTROL\_CAP**](ksproperty-videocontrol-caps.md)

视频捕获微型驱动程序可以根据需要实现以下属性：

[**KSPROPERTY\_VIDEOCONTROL\_实际\_帧\_速率**](ksproperty-videocontrol-actual-frame-rate.md)

[**KSPROPERTY\_VIDEOCONTROL\_FRAME\_RATES**](ksproperty-videocontrol-frame-rates.md)

[**KSPROPERTY\_VIDEOCONTROL\_模式**](ksproperty-videocontrol-mode.md)

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow 接口

没有 DirectShow 界面提供访问此属性集。

 

 





