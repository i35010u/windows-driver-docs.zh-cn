---
title: PROPSETID \_ VIDCAP \_ CAMERACONTROL
description: PROPSETID \_ VIDCAP \_ CAMERACONTROL
ms.assetid: 8899a474-fa6f-4d5c-bd68-2433428bb5c5
keywords:
- KSPROPERTY_VIDCAP_CAMERACONTROL
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: b60ea6e949c7ad352df2524f6d1125941219affa
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186757"
---
# <a name="propsetid_vidcap_cameracontrol"></a>PROPSETID \_ VIDCAP \_ CAMERACONTROL

PROPSETID \_ VIDCAP \_ CAMERACONTROL 属性集控制照相机设备设置。 它提供的控件是 ITU-T 标准的子集。

\_Ksmedia 中的 KSPROPERTY VIDCAP \_ CAMERACONTROL 枚举指定此集的属性。

对此属性集的支持是可选的，只应由提供相机控制设置的设备微型驱动程序来实现。 有关详细信息，请参阅 [ITU](https://www.itu.int/) 网站。

在 USB 视频类之前，此枚举包含以下属性：

[**KSPROPERTY \_ CAMERACONTROL \_ 曝露**](ksproperty-cameracontrol-exposure.md)

[**KSPROPERTY \_ CAMERACONTROL \_**](ksproperty-cameracontrol-focus.md)

[**KSPROPERTY \_ CAMERACONTROL \_ IRIS**](ksproperty-cameracontrol-iris.md)

[**KSPROPERTY \_ CAMERACONTROL \_ 缩放**](ksproperty-cameracontrol-zoom.md)

[**KSPROPERTY \_ CAMERACONTROL \_ 平移**](ksproperty-cameracontrol-pan.md)

[**KSPROPERTY \_ CAMERACONTROL \_ 横滚**](ksproperty-cameracontrol-roll.md)

[**KSPROPERTY \_ CAMERACONTROL \_ 倾斜**](ksproperty-cameracontrol-tilt.md)

由于引入了 [USB 视频类驱动程序](./usb-video-class-driver.md)，以下属性已添加到 KSPROPERTY \_ VIDCAP \_ CAMERACONTROL 枚举中。

[**KSPROPERTY \_ CAMERACONTROL \_ SCANMODE**](ksproperty-cameracontrol-scanmode.md)

[**KSPROPERTY \_ CAMERACONTROL \_ 隐私**](ksproperty-cameracontrol-privacy.md)

[**KSPROPERTY \_ CAMERACONTROL \_ PANTILT**](ksproperty-cameracontrol-pantilt.md)

[**KSPROPERTY \_ CAMERACONTROL \_ 全景 \_ 相对**](ksproperty-cameracontrol-pan-relative.md)

[**KSPROPERTY \_ CAMERACONTROL \_ 倾斜 \_**](ksproperty-cameracontrol-tilt-relative.md)

[**KSPROPERTY \_ CAMERACONTROL \_ \_ 相对**](ksproperty-cameracontrol-roll-relative.md)

[**KSPROPERTY \_ CAMERACONTROL \_ ZOOM \_ 相对**](ksproperty-cameracontrol-zoom-relative.md)

[**KSPROPERTY \_ CAMERACONTROL \_ 曝光 \_ 相对**](ksproperty-cameracontrol-exposure-relative.md)

[**KSPROPERTY \_ CAMERACONTROL \_ IRIS \_ 相对**](ksproperty-cameracontrol-iris-relative.md)

[**KSPROPERTY \_ CAMERACONTROL \_ 焦点 \_ 相对**](ksproperty-cameracontrol-focus-relative.md)

[**KSPROPERTY \_ CAMERACONTROL \_ PANTILT \_ 相对**](ksproperty-cameracontrol-pantilt-relative.md)

[**KSPROPERTY \_ CAMERACONTROL \_ 焦距 \_**](ksproperty-cameracontrol-focal-length.md)

[**KSPROPERTY \_ CAMERACONTROL \_ 自动 \_ 曝光 \_ 优先级**](ksproperty-cameracontrol-auto-exposure-priority.md)

DirectShow **IAMCameraControl** 接口 (参阅 Windows 软件开发工具包中的 Microsoft DirectShow 文档 (SDK) # A3 提供对此集的属性的访问权限。

## <a name="windows8-extended-camera-control-properties"></a>Windows 8 扩展相机控制属性

从 Windows 8 开始，用户模式客户端支持使用这些附加属性来获取或设置照相机的控制设置：

[**KSPROPERTY \_ CAMERACONTROL \_ FLASH \_ 属性**](ksproperty-cameracontrol-flash-property.md)

[**KSPROPERTY \_ CAMERACONTROL \_ 图像 \_ PIN \_ 功能 \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s)

[**KSPROPERTY \_ CAMERACONTROL \_ \_ \_ 感兴趣的区域 \_ 属性**](ksproperty-cameracontrol-region-of-interest-property.md)

[**KSPROPERTY \_ CAMERACONTROL \_ 视频 \_ 稳定 \_ 模式 \_ 属性**](ksproperty-cameracontrol-video-stabilization-mode-property.md)