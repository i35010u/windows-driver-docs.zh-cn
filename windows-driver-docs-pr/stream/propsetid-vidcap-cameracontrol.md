---
title: PROPSETID\_VIDCAP\_CAMERACONTROL
description: PROPSETID\_VIDCAP\_CAMERACONTROL
ms.assetid: 8899a474-fa6f-4d5c-bd68-2433428bb5c5
keywords:
- KSPROPERTY_VIDCAP_CAMERACONTROL
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 851416fefc0246c3c30b10127fb42edee7535630
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379070"
---
# <a name="propsetidvidcapcameracontrol"></a>PROPSETID\_VIDCAP\_CAMERACONTROL


## <span id="ddk_propsetid_vidcap_cameracontrol_ks"></span><span id="DDK_PROPSETID_VIDCAP_CAMERACONTROL_KS"></span>


PROPSETID\_VIDCAP\_CAMERACONTROL 属性设置控制照相机设备设置。 它提供的控件是 ITU T.RDC 标准的子集。

KSPROPERTY\_VIDCAP\_中 Ksmedia.h CAMERACONTROL 枚举指定此集的属性。

支持设置此属性是可选的应仅由微型驱动程序的产品/服务照相机控件设置的设备。 有关详细信息，请参阅[ITU](https://go.microsoft.com/fwlink/p/?linkid=8741)网站。

在 USB 视频类之前此枚举包含以下属性：

[**KSPROPERTY\_CAMERACONTROL\_风险**](ksproperty-cameracontrol-exposure.md)

[**KSPROPERTY\_CAMERACONTROL\_焦点**](ksproperty-cameracontrol-focus.md)

[**KSPROPERTY\_CAMERACONTROL\_鸢尾花**](ksproperty-cameracontrol-iris.md)

[**KSPROPERTY\_CAMERACONTROL\_ZOOM**](ksproperty-cameracontrol-zoom.md)

[**KSPROPERTY\_CAMERACONTROL\_平移**](ksproperty-cameracontrol-pan.md)

[**KSPROPERTY\_CAMERACONTROL\_回滚**](ksproperty-cameracontrol-roll.md)

[**KSPROPERTY\_CAMERACONTROL\_倾斜**](ksproperty-cameracontrol-tilt.md)

通过引入[USB 视频类驱动程序](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver)，以下属性已添加到 KSPROPERTY\_VIDCAP\_CAMERACONTROL 枚举。 在 Windows Vista 和更高版本的 Windows 中支持这些属性：

[**KSPROPERTY\_CAMERACONTROL\_扫描模式**](ksproperty-cameracontrol-scanmode.md)

[**KSPROPERTY\_CAMERACONTROL\_隐私**](ksproperty-cameracontrol-privacy.md)

[**KSPROPERTY\_CAMERACONTROL\_PANTILT**](ksproperty-cameracontrol-pantilt.md)

[**KSPROPERTY\_CAMERACONTROL\_PAN\_RELATIVE**](ksproperty-cameracontrol-pan-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_TILT\_RELATIVE**](ksproperty-cameracontrol-tilt-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_ROLL\_RELATIVE**](ksproperty-cameracontrol-roll-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_ZOOM\_RELATIVE**](ksproperty-cameracontrol-zoom-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_EXPOSURE\_RELATIVE**](ksproperty-cameracontrol-exposure-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_鸢尾花\_相对**](ksproperty-cameracontrol-iris-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_焦点\_相对**](ksproperty-cameracontrol-focus-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_PANTILT\_RELATIVE**](ksproperty-cameracontrol-pantilt-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_焦点\_长度**](ksproperty-cameracontrol-focal-length.md)

[**KSPROPERTY\_CAMERACONTROL\_自动\_暴露\_优先级**](ksproperty-cameracontrol-auto-exposure-priority.md)

DirectShow **IAMCameraControl**接口 （请参阅 Microsoft DirectShow 文档中 Windows 软件开发工具包 (SDK)） 提供对此集的属性的访问。

## <a name="span-idwindows8extendedcameracontrolpropertiesspanspan-idwindows8extendedcameracontrolpropertiesspanspan-idwindows8extendedcameracontrolpropertiesspanwindows8-extended-camera-control-properties"></a><span id="Windows_8_extended_camera_control_properties"></span><span id="windows_8_extended_camera_control_properties"></span><span id="WINDOWS_8_EXTENDED_CAMERA_CONTROL_PROPERTIES"></span>Windows 8 扩展相机控件属性


从 Windows 8 开始，对于要获取或设置照相机的控制设置的用户模式下客户端支持这些附加属性：

[**KSPROPERTY\_CAMERACONTROL\_闪存\_属性**](ksproperty-cameracontrol-flash-property.md)

[**KSPROPERTY\_CAMERACONTROL\_映像\_PIN\_功能\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s)

[**KSPROPERTY\_CAMERACONTROL\_区域\_OF\_感兴趣\_属性**](ksproperty-cameracontrol-region-of-interest-property.md)

[**KSPROPERTY\_CAMERACONTROL\_视频\_稳定\_模式\_属性**](ksproperty-cameracontrol-video-stabilization-mode-property.md)

 

 





