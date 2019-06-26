---
title: PROPSETID\_VIDCAP\_VIDEOPROCAMP
description: PROPSETID\_VIDCAP\_VIDEOPROCAMP
ms.assetid: ea1d9c96-b1a5-4849-b607-4c508a526512
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5373370c0e7ce409577b4c8655466334ea04b4d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385695"
---
# <a name="propsetidvidcapvideoprocamp"></a>PROPSETID\_VIDCAP\_VIDEOPROCAMP


## <span id="ddk_propsetid_vidcap_videoprocamp_ks"></span><span id="DDK_PROPSETID_VIDCAP_VIDEOPROCAMP_KS"></span>


PROPSETID\_VIDCAP\_VIDEOPROCAMP 属性设置控件可以调整图像颜色特性的模拟或数字信号的设备。

KSPROPERTY\_VIDCAP\_中的 VIDEOPROCAMP 枚举*ksmedia.h*指定此集的属性。

支持设置此属性是可选的应仅通过允许调整亮度、 对比度、 色调和其他图像质量设置的设备来实现。

在 USB 视频类之前此枚举包含以下属性项：

[**KSPROPERTY\_VIDEOPROCAMP\_背景光\_补偿**](ksproperty-videoprocamp-backlight-compensation.md)

[**KSPROPERTY\_VIDEOPROCAMP\_亮度**](ksproperty-videoprocamp-brightness.md)

[**KSPROPERTY\_VIDEOPROCAMP\_COLORENABLE**](ksproperty-videoprocamp-colorenable.md)

[**KSPROPERTY\_VIDEOPROCAMP\_对比度**](ksproperty-videoprocamp-contrast.md)

[**KSPROPERTY\_VIDEOPROCAMP\_GAMMA**](ksproperty-videoprocamp-gamma.md)

[**KSPROPERTY\_VIDEOPROCAMP\_HUE**](ksproperty-videoprocamp-hue.md)

[**KSPROPERTY\_VIDEOPROCAMP\_饱和度**](ksproperty-videoprocamp-saturation.md)

[**KSPROPERTY\_VIDEOPROCAMP\_锐度**](ksproperty-videoprocamp-sharpness.md)

[**KSPROPERTY\_VIDEOPROCAMP\_WHITEBALANCE**](ksproperty-videoprocamp-whitebalance.md)

[**KSPROPERTY\_VIDEOPROCAMP\_获得**](ksproperty-videoprocamp-gain.md)

通过引入[USB 视频类驱动程序](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver)，以下属性已添加到 KSPROPERTY\_VIDCAP\_VIDEOPROCAMP 枚举：

[**KSPROPERTY\_VIDEOPROCAMP\_数字\_乘数**](ksproperty-videoprocamp-digital-multiplier.md)

[**KSPROPERTY\_VIDEOPROCAMP\_数字\_乘数\_限制**](ksproperty-videoprocamp-digital-multiplier-limit.md)

[**KSPROPERTY\_VIDEOPROCAMP\_WHITEBALANCE\_COMPONENT**](ksproperty-videoprocamp-whitebalance-component.md)

[**KSPROPERTY\_VIDEOPROCAMP\_POWERLINE\_FREQUENCY**](ksproperty-videoprocamp-powerline-frequency.md)

每个属性中 PROPSETID\_VIDEOPROCAMP 属性集包括的范围和默认值。 现实世界单位，以允许以编程方式控制的参数中定义的属性集的范围。 每个设备可以定义此范围，以及步骤大小的子集。 这允许控件，如滑块和滚动条，以编程，以便为每个步骤的可视效果。

例如，亮度的总体理论范围被指到 100 个过期单位-100。 过期是 NTSC 定义的度量值的视频的级别，其中 0 对应于消隐功能或完全黑色级别，100 表示纯白色。 如果 VideoProcAmp 无法转移 （可能是由完全涵盖相机镜头生成） 的纯黑色输入的信号并使其显示为纯模式，其范围将是 0 到 100 过期。

大多数 VideoProcAmps 实际提供有限的亮度控制的范围。 度量值范围的一种方法是涵盖相机镜头和调整的范围内确定输出信号，然后将此规范化到过期单位。 在计算范围之后，可以通过采用最大和最小值，并调整步骤数除以派生单步执行值 **（最大值 + 最小值） /N 调整步骤**。

请注意中的属性集使用的值乘以 100 以提供改进的粒度。

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow 接口

DirectShow **IAMVideoProcAmp**接口 （请参阅 Microsoft Windows SDK 中的 DirectShow 文档） 提供对此集的属性的访问。

 

 





