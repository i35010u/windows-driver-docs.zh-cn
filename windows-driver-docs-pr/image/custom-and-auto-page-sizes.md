---
title: 自定义的和自动设置的页面大小
description: 自定义的和自动设置的页面大小
ms.assetid: a1f5f78d-fc05-4a7e-9d19-c7f40302b85f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b5814f99733ab2e87c6588e29258921ef9fb39f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360864"
---
# <a name="custom-and-auto-page-sizes"></a>自定义的和自动设置的页面大小


应用程序可以设置页面大小通过自动检测扫描仪或通过自定义值。 应用程序使用的方法由[ **WIA\_IPS\_页\_大小**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-page-size)属性，可以采用值 WIA\_页\_自动或 WIA\_页\_自定义。

如果应用程序设置 WIA\_IPS\_页面\_WIA 以外的任何值的大小\_页\_自定义，WIA 微型驱动程序应调整 WIA 的值\_IP\_页\_宽度和 WIA\_IPS\_页\_高度和页面的尺寸，以英寸为单位的千分之几秒 (。 001)。 微型驱动程序还应调整 WIA 的值\_IPS\_大 XEXTENT 和 WIA\_IP\_YEXTENT 到页面的尺寸，以像素为单位。

如果扩展盘区设置 (WIA\_IPS\_大 XEXTENT 或 WIA\_IP\_YEXTENT) 更改为值执行*不*与当前的页面大小设置匹配，应更改微型驱动程序值 WIA\_IP\_页面\_大小属性设置为 WIA\_页\_自定义。 微型驱动程序还应修改 WIA\_IPS\_页面\_宽度或 WIA\_IP\_页\_高度，以便与新的范围内设置。

如果应用程序设置 WIA\_IPS\_页\_大小属性设置为 WIA\_页\_自定义的当前选择区域不受影响。 WIA 微型驱动程序应获取当前的图像布局中，从当前的设置开始[ **WIA\_IPS\_XPOS** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xpos)并[ **WIA\_IPS\_YPOS** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-ypos)属性。 如果页面大小设置而导致的选择区域，将扫描程序的平台之外，微型驱动程序必须自动调整值 WIA\_IPS\_XPOS 和 WIA\_IP\_YPOS 属性的有效设置。 如果 WIA\_IPS\_页面\_大小和 WIA\_IP\_方向属性设置在同一时间并且它们是无效的它们应用结合使用时，微型驱动程序应失败通过返回中的错误的应用程序的设置[ **IWiaMiniDrv::drvValidateItemProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)方法。

当启用了自动页大小检测时，驱动程序应提供的图像数据传输完成后，才精确的图像维度信息。 对于基于流的传输模式，该驱动程序需要更新映像标头传输结束时将图像尺寸。 在新的会话，WIA 的值开头\_IPS\_页面\_大小属性应始终设置为 WIA 以外的值\_页\_自动。

当 WIA\_页上\_自动设置为当前 WIA\_IP\_页\_大小值，该驱动程序可能需要首先将包含泛型图像尺寸，映像标头，然后将映像传递数据，然后转到传输流的起点使用的实际图像尺寸 （找到已完成扫描后） 和移动流索引返回到流的末尾更新映像标头。

当 WIA\_页\_自动设置 （所选为默认值由驱动程序或由应用程序设置），该应用程序不应尝试处理图像维度映像标头描述直到整个图像传输已完成。

**请注意**  WIA 服务中的兼容性层不会添加支持 WIA\_IP\_页\_到如果属性不是从 Windows XP WIA 的设备转换的 ADF 项的大小支持的设备的子项目。 应用程序不应期望 ADF 项始终支持此属性，如果应始终检查 WIA\_IPS\_页\_在运行时支持大小。 （通常情况下，应用程序应检查的任何属性都是协商的支持。）

 

 

 




