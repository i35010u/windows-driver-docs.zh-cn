---
title: PROPSETID\_VIDCAP\_CAMERACONTROL
description: PROPSETID\_VIDCAP\_CAMERACONTROL
ms.assetid: 8899a474-fa6f-4d5c-bd68-2433428bb5c5
keywords:
- KSPROPERTY_VIDCAP_CAMERACONTROL
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87102b025557ca5069915795ba45a601e78d6afc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823725"
---
# <a name="propsetid_vidcap_cameracontrol"></a>PROPSETID\_VIDCAP\_CAMERACONTROL


## <span id="ddk_propsetid_vidcap_cameracontrol_ks"></span><span id="DDK_PROPSETID_VIDCAP_CAMERACONTROL_KS"></span>


PROPSETID\_VIDCAP\_CAMERACONTROL 属性集控制照相机设备设置。 它提供的控件是 ITU-T 标准的子集。

Ksmedia 中的 KSPROPERTY\_VIDCAP\_CAMERACONTROL 枚举指定此集的属性。

对此属性集的支持是可选的，只应由提供相机控制设置的设备微型驱动程序来实现。 有关详细信息，请参阅[ITU](https://go.microsoft.com/fwlink/p/?linkid=8741)网站。

在 USB 视频类之前，此枚举包含以下属性：

[**KSPROPERTY\_CAMERACONTROL\_泄露**](ksproperty-cameracontrol-exposure.md)

[**KSPROPERTY\_CAMERACONTROL\_焦点**](ksproperty-cameracontrol-focus.md)

[**KSPROPERTY\_CAMERACONTROL\_IRIS**](ksproperty-cameracontrol-iris.md)

[**KSPROPERTY\_CAMERACONTROL\_缩放**](ksproperty-cameracontrol-zoom.md)

[**KSPROPERTY\_CAMERACONTROL\_平移**](ksproperty-cameracontrol-pan.md)

[**KSPROPERTY\_CAMERACONTROL\_滚动**](ksproperty-cameracontrol-roll.md)

[**KSPROPERTY\_CAMERACONTROL\_倾斜**](ksproperty-cameracontrol-tilt.md)

由于引入了[USB 视频类驱动程序](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver)，以下属性已添加到 KSPROPERTY\_VIDCAP\_CAMERACONTROL 枚举中。 Windows Vista 和更高版本的 Windows 支持以下属性：

[**KSPROPERTY\_CAMERACONTROL\_SCANMODE**](ksproperty-cameracontrol-scanmode.md)

[**KSPROPERTY\_CAMERACONTROL\_隐私**](ksproperty-cameracontrol-privacy.md)

[**KSPROPERTY\_CAMERACONTROL\_PANTILT**](ksproperty-cameracontrol-pantilt.md)

[**KSPROPERTY\_CAMERACONTROL\_平移\_相对**](ksproperty-cameracontrol-pan-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_倾斜度\_相对**](ksproperty-cameracontrol-tilt-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_滚动\_相对**](ksproperty-cameracontrol-roll-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_缩放\_相对**](ksproperty-cameracontrol-zoom-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_泄露\_相对**](ksproperty-cameracontrol-exposure-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_IRIS\_相对**](ksproperty-cameracontrol-iris-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_焦点\_相对**](ksproperty-cameracontrol-focus-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_PANTILT\_相对**](ksproperty-cameracontrol-pantilt-relative.md)

[**KSPROPERTY\_CAMERACONTROL\_焦\_长度**](ksproperty-cameracontrol-focal-length.md)

[**KSPROPERTY\_CAMERACONTROL\_自动\_公开\_优先级**](ksproperty-cameracontrol-auto-exposure-priority.md)

DirectShow **IAMCameraControl**接口（请参阅 Windows 软件开发工具包（SDK）中的 Microsoft DirectShow 文档）提供对此集的属性的访问权限。

## <a name="span-idwindows_8_extended_camera_control_propertiesspanspan-idwindows_8_extended_camera_control_propertiesspanspan-idwindows_8_extended_camera_control_propertiesspanwindows8-extended-camera-control-properties"></a><span id="Windows_8_extended_camera_control_properties"></span><span id="windows_8_extended_camera_control_properties"></span><span id="WINDOWS_8_EXTENDED_CAMERA_CONTROL_PROPERTIES"></span>Windows 8 扩展相机控制属性


从 Windows 8 开始，用户模式客户端支持使用这些附加属性来获取或设置照相机的控制设置：

[**KSPROPERTY\_CAMERACONTROL\_闪存\_属性**](ksproperty-cameracontrol-flash-property.md)

[**KSPROPERTY\_CAMERACONTROL\_映像\_PIN\_功能\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s)

[**KSPROPERTY\_CAMERACONTROL\_区域\_\_兴趣\_属性**](ksproperty-cameracontrol-region-of-interest-property.md)

[**KSPROPERTY\_CAMERACONTROL\_视频\_稳定性\_模式\_属性**](ksproperty-cameracontrol-video-stabilization-mode-property.md)

 

 





