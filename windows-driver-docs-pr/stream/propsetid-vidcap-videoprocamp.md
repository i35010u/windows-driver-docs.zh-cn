---
title: PROPSETID \_ VIDCAP \_ VIDEOPROCAMP
description: PROPSETID \_ VIDCAP \_ VIDEOPROCAMP
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8af75c70b527d86eaa76f25205c8853b1962d74a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818755"
---
# <a name="propsetid_vidcap_videoprocamp"></a>PROPSETID \_ VIDCAP \_ VIDEOPROCAMP


## <span id="ddk_propsetid_vidcap_videoprocamp_ks"></span><span id="DDK_PROPSETID_VIDCAP_VIDEOPROCAMP_KS"></span>


PROPSETID \_ VIDCAP \_ VIDEOPROCAMP 属性集控制可调整模拟或数字信号的图像颜色属性的设备。

\_Ksmedia 中的 KSPROPERTY VIDCAP \_ VIDEOPROCAMP *ksmedia.h* 枚举指定此集的属性。

对此属性集的支持是可选的，只应由允许调整亮度、对比度、色相和其他图像质量设置的设备来实现。

在 USB 视频类之前，此枚举包含以下属性项：

[**KSPROPERTY \_ VIDEOPROCAMP \_ 背光 \_ 补偿**](ksproperty-videoprocamp-backlight-compensation.md)

[**KSPROPERTY \_ VIDEOPROCAMP \_ 亮度**](ksproperty-videoprocamp-brightness.md)

[**KSPROPERTY \_ VIDEOPROCAMP \_ COLORENABLE**](ksproperty-videoprocamp-colorenable.md)

[**KSPROPERTY \_ VIDEOPROCAMP \_ 对比度**](ksproperty-videoprocamp-contrast.md)

[**KSPROPERTY \_ VIDEOPROCAMP \_ 伽玛**](ksproperty-videoprocamp-gamma.md)

[**KSPROPERTY \_ VIDEOPROCAMP \_ 色调**](ksproperty-videoprocamp-hue.md)

[**KSPROPERTY \_ VIDEOPROCAMP \_ 饱和度**](ksproperty-videoprocamp-saturation.md)

[**KSPROPERTY \_ VIDEOPROCAMP \_ 锐度**](ksproperty-videoprocamp-sharpness.md)

[**KSPROPERTY \_ VIDEOPROCAMP \_ WHITEBALANCE**](ksproperty-videoprocamp-whitebalance.md)

[**KSPROPERTY \_ VIDEOPROCAMP \_ 增益**](ksproperty-videoprocamp-gain.md)

由于引入了 [USB 视频类驱动程序](./usb-video-class-driver.md)，以下属性已添加到 KSPROPERTY \_ VIDCAP \_ VIDEOPROCAMP 枚举：

[**KSPROPERTY \_ VIDEOPROCAMP \_ 数字 \_ 乘数**](ksproperty-videoprocamp-digital-multiplier.md)

[**KSPROPERTY \_ VIDEOPROCAMP \_ 数字 \_ 乘数 \_ 限制**](ksproperty-videoprocamp-digital-multiplier-limit.md)

[**KSPROPERTY \_ VIDEOPROCAMP \_ WHITEBALANCE \_ 组件**](ksproperty-videoprocamp-whitebalance-component.md)

[**KSPROPERTY \_ VIDEOPROCAMP \_ POWERLINE \_ FREQUENCY**](ksproperty-videoprocamp-powerline-frequency.md)

PROPSETID VIDEOPROCAMP 属性集中的每个属性都 \_ 包括一个范围和默认值。 在实际单元中定义属性集的范围，以允许以编程方式控制参数。 每个设备都可以定义此范围的子集以及步长大小。 这允许对控件（如滑块和滚动条）进行编程，以便为每个步骤提供可见效果。

例如，亮度的总体理论范围定义为-100 到 100 PROTOKOL 单元。 PROTOKOL 是视频级别的 NTSC 定义度量值，其中0对应于消隐或全黑级别，100表示纯白色。 如果 VideoProcAmp 能够转移纯黑色输入信号 (可能会通过完全覆盖相机镜头而生成) 并使其显示为纯白色，则其范围将为0到 100 PROTOKOL。

大多数 VideoProcAmps 实际上提供有限范围的亮度控制。 测量范围的一种方法是覆盖相机镜头并确定调整范围内的输出信号，然后将其规范化为 PROTOKOL 单元。 计算该范围后，可以通过获取最大值和最小值并除以调整步骤数 **(max + min) /n 调整步骤** 来派生步进值。

请注意，在属性集中使用的值乘以100以提高粒度。

### <a name="span-iddirectshow_interfacespanspan-iddirectshow_interfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow 接口

DirectShow **IAMVideoProcAmp** 接口 (参阅 Microsoft Windows SDK 中的 directshow 文档) 提供对此集的属性的访问权限。

 

