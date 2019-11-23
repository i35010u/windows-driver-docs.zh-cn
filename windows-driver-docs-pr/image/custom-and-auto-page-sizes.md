---
title: 自定义的和自动设置的页面大小
description: 自定义的和自动设置的页面大小
ms.assetid: a1f5f78d-fc05-4a7e-9d19-c7f40302b85f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a91fbc8f2a0483b7134f2f392dcca78c773e0703
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840863"
---
# <a name="custom-and-auto-page-sizes"></a>自定义的和自动设置的页面大小


应用程序可以通过扫描程序自动检测或通过自定义值来设置页面大小。 应用程序使用的方法由[**WIA\_IPS\_页面\_大小**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-page-size)属性确定，该属性可以将值 WIA\_页面\_自动或 WIA\_\_自定义。

如果某个应用程序将 "WIA\_IPS\_" 页\_大小设置为 WIA\_页面\_"自定义" 以外的任何值，则 WIA 微型驱动程序应将 "WIA\_的值"\_"\_宽度" 和 "WIA\_IPS\_\_ 微型驱动程序还应将 WIA\_IPS\_XEXTENT 和 WIA\_IP\_YEXTENT 的值调整为以像素为单位的。

如果扩展盘区设置（WIA\_IPS\_XEXTENT 或 WIA\_IPS\_YEXTENT）更改为与当前页面大小设置*不*匹配的值，则微型驱动程序应将 "WIA\_IPS\_页\_大小" 属性的值更改为 wia\_"自定义"。\_ 微型驱动程序还应修改 WIA\_IPS\_页面\_宽度或 WIA\_IP\_"\_高度" 以同意新的范围设置。

如果应用程序将 WIA\_IPS\_"\_大小" 属性设置为 "WIA\_" 页\_"自定义"，则不会影响当前选定区域。 WIA 微型驱动程序应从[**WIA\_ips\_XPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xpos)和[**WIA\_ip\_YPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-ypos)属性的当前设置开始，获取当前的图像布局。 如果页面大小设置导致选择区域位于扫描仪平台外，则微型驱动程序必须自动将 WIA\_IP\_XPOS 和 WIA\_\_IPS 的值调整为有效设置。 如果 WIA\_IPS\_页\_大小和 WIA\_IP\_方向属性同时设置并且它们在组合应用时无效，则微型驱动程序应通过在[**IWiaMiniDrv：:D rvvalidateitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)方法中返回错误来使应用程序的设置失败。

当启用自动页大小检测时，驱动程序只应在完成图像数据传输后提供准确的映像维度信息。 对于基于流的传输，驱动程序应在传输结束时更新图像标头中的图像维度。 新会话开始时，WIA\_IPS\_页\_大小属性的值应始终设置为 WIA\_页\_自动值。

当 WIA\_页面\_自动设置为当前 WIA\_IP\_页面\_大小值，驱动程序可能需要首先传输包含通用图像维度的图像标题，然后传输图像数据，然后返回到传输流的开始位置，使用实际图像尺寸更新图像标头（在扫描完成后找到），并将流索引移回流的末尾。

如果设置了 WIA\_页面\_自动设置（由驱动程序选择的默认值或应用程序设置的值），则应用程序不应尝试处理图像标题所描述的图像尺寸，直到完成整个图像传输。

**请注意**  wia 服务中的兼容性层不会将对 WIA\_IPS\_页\_大小的支持添加到从 WINDOWS XP WIA 设备转换的 ADF 项（如果该设备的子项目不支持）。 应用程序不应期望 ADF 项始终支持此属性，并且应始终检查是否支持 WIA\_IPS\_页\_大小在运行时是否受支持。 （通常情况下，应用程序应检查是否支持要协商的任何属性。）

 

 

 




