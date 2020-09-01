---
title: 自定义的和自动设置的页面大小
description: 自定义的和自动设置的页面大小
ms.assetid: a1f5f78d-fc05-4a7e-9d19-c7f40302b85f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38de471b3232f756392e0ffbf3d225b950b7c4e8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191709"
---
# <a name="custom-and-auto-page-sizes"></a>自定义的和自动设置的页面大小


应用程序可以通过扫描程序自动检测或通过自定义值来设置页面大小。 应用程序使用的方法由 " [**wia \_ ip \_ 页面 \_ 大小**](./wia-ips-page-size.md) " 属性确定，该属性可以采用 "wia \_ 页面 \_ 自动" 或 "wia \_ 页面 \_ 自定义" 值。

如果应用程序将 WIA \_ ip \_ 页面 \_ 大小设置为 wia \_ 页面 \_ 自定义以外的任何值，则 wia 微型驱动程序应将 WIA \_ ip \_ 页面 \_ 宽度和 wia ip 页面高度的值以 \_ \_ \_ ( 英寸的千分之几分之) 调整到页面的尺寸。 微型驱动程序还应将 WIA \_ ip \_ XEXTENT 和 wia ips YEXTENT 的值 \_ 调整 \_ 到页面的尺寸（以像素为单位）。

如果 (WIA \_ ip \_ XEXTENT 或 wia \_ ips YEXTENT) 的区设置 \_ 更改为与当前页面大小设置 *不* 匹配的值，则微型驱动程序应将 "wia \_ ip 页面大小" 属性的值更改 \_ 为 " \_ wia \_ 页面 \_ 自定义"。 微型驱动程序还应修改 WIA \_ ip \_ 页面 \_ 宽度或 wia \_ ip \_ 页面 \_ 高度，以同意新的范围设置。

如果应用程序将 "WIA \_ ip \_ 页面 \_ 大小" 属性设置为 \_ "wia 页面 \_ 自定义"，则当前选择区域不受影响。 WIA 微型驱动程序应从 [**wia \_ ip \_ XPOS**](./wia-ips-xpos.md) 和 [**wia \_ ip \_ YPOS**](./wia-ips-ypos.md) 属性的当前设置开始，获取当前的图像布局。 如果页面大小设置导致选择区域位于扫描仪平台外，则微型驱动程序必须自动将 WIA \_ ips \_ XPOS 和 wia ips 属性的值调整 \_ \_ 为有效设置。 如果 WIA \_ ip \_ 页面 \_ 大小和 wia \_ ips \_ 方向属性同时设置并且它们在组合应用时无效，则微型驱动程序应通过在 [**IWiaMiniDrv：:d rvvalidateitemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties) 方法中返回错误来使应用程序的设置失败。

当启用自动页大小检测时，驱动程序只应在完成图像数据传输后提供准确的映像维度信息。 对于基于流的传输，驱动程序应在传输结束时更新图像标头中的图像维度。 新会话开始时，"WIA \_ ip 页面大小" 属性的值 \_ \_ 应始终设置为 "wia 页面自动" 以外的值 \_ \_ 。

当 WIA \_ 页面 " \_ 自动" 设置为 "当前 WIA \_ ip \_ 页面大小" 值时 \_ ，驱动程序可能需要首先传输包含通用图像维度的图像标题，然后传输图像数据，然后返回到传输流的开始位置，使用实际图像尺寸更新图像标头 (在扫描完成后) ，然后将流索引移回流的末尾。

如果 \_ 将 WIA 页面 \_ "自动" 设置 (选择为驱动程序的默认值或由应用程序) 设置，则应用程序不应尝试处理图像标题所描述的图像尺寸，直到整个图像传输完成。

**注意**   如果设备的子项目不支持属性，则 WIA 服务内的兼容性层不会将对 WIA \_ ip 页面大小的支持添加 \_ \_ 到从 Windows XP WIA 设备转换的 ADF 项。 应用程序不应期望 ADF 项始终支持此属性，并且应始终检查是否 \_ 支持 WIA ip \_ 页面 \_ 大小。  (通常情况下，应用程序应检查是否支持要协商的任何属性。 ) 

 

 

