---
title: WIA 扫描程序微型驱动程序的属性
description: WIA 扫描程序微型驱动程序的属性
ms.assetid: 9de8694a-0d19-4945-b0c1-a3c4bc71dad3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a54c4888ebb3eff9a2951f22886d7852dcc35b03
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374319"
---
# <a name="properties-for-wia-scanner-minidrivers"></a>WIA 扫描程序微型驱动程序的属性





以下列表包含所有是唯一的 WIA 扫描程序微型驱动程序的 WIA 属性。

### <a name="required-properties-on-scanner-root-items-microsoft-windows-xp-and-windows-me"></a>所需属性上扫描程序的根项 (Microsoft Windows XP 和 Windows Me)

WIA 微型驱动程序提供以下属性：

[**WIA\_DPS\_OPTICAL\_XRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-optical-xres)

[**WIA\_DPS\_光学\_YRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-optical-yres)

### <a name="optional-properties-on-scanner-root-items-windows-xp-and-windows-me"></a>扫描程序的可选属性根项 (Windows XP 和 Windows Me)

WIA 微型驱动程序提供以下属性：

[**WIA\_DPS\_DITHER\_PATTERN\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-dither-pattern-data)

[**WIA\_DPS\_DITHER\_SELECT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-dither-select)

[**WIA\_DPS\_FILTER\_SELECT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-filter-select)

[**WIA\_DPS\_MAX\_SCAN\_TIME**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-max-scan-time)

[**WIA\_DPS\_PAD\_颜色**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-pad-color)

[**WIA\_DPS\_辊\_颜色**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-platen-color)

[**WIA\_DPS\_显示\_预览\_控件**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-show-preview-control)

### <a name="required-properties-on-scanner-child-items-able-to-transfer-data"></a>在扫描程序的子项目能够将数据传输所需的属性

WIA 微型驱动程序提供以下属性：

[**WIA\_IP\_亮度**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-brightness)

[**WIA\_IPS\_CONTRAST**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-contrast)

[**WIA\_IPS\_CUR\_INTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-cur-intent)

[**WIA\_IPS\_PHOTOMETRIC\_INTERP**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-photometric-interp)

[**WIA\_IPS\_XEXTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xextent)

[**WIA\_IPS\_XPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xpos)

[**WIA\_IPS\_XRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xres)

[**WIA\_IPS\_YEXTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yextent)

[**WIA\_IPS\_YPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-ypos)

[**WIA\_IPS\_YRES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yres)

### <a name="optional-properties-on-scanner-child-items-able-to-transfer-data"></a>扫描程序的子项目能够将数据传输的可选属性

WIA 微型驱动程序提供以下属性：

[**WIA\_DPS\_PAGE\_HEIGHT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-page-height)

[**WIA\_DPS\_PAGE\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-page-size)

[**WIA\_DPS\_PAGE\_WIDTH**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-page-width)

[**WIA\_IPS\_INVERT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-invert)

[**WIA\_IPS\_MIRROR**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-mirror)

[**WIA\_IP\_方向**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-orientation)

[**WIA\_IP\_旋转**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-rotation)

[**WIA\_IP\_阈值**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-threshold)

[**WIA\_IPS\_WARM\_UP\_TIME**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-warm-up-time)

### <a name="required-properties-on-flatbed-scanner-root-items-windows-xp-and-windows-me"></a>所需属性上平板扫描仪根项 (Windows XP 和 Windows Me)

WIA 微型驱动程序提供以下属性：

[**WIA\_DPS\_水平\_平台\_注册**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-horizontal-bed-registration)

[**WIA\_DPS\_水平\_平台\_大小**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-horizontal-bed-size)

[**WIA\_DPS\_预览**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-preview)

[**WIA\_DPS\_垂直\_平台\_注册**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-vertical-bed-registration)

[**WIA\_DPS\_VERTICAL\_BED\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-vertical-bed-size)

### <a name="required-properties-on-document-feeder-scanner-root-items-windows-xp-and-windows-me"></a>所需属性文档送纸器扫描程序的根项 (Windows XP 和 Windows Me)

WIA 微型驱动程序提供以下属性：

[**WIA\_DPS\_文档\_处理\_功能**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-capabilities)

[**WIA\_DPS\_文档\_处理\_选择**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-select)

[**WIA\_DPS\_文档\_处理\_状态**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-status)

[**WIA\_DPS\_HORIZONTAL\_SHEET\_FEED\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-horizontal-sheet-feed-size)

[**WIA\_DPS\_MIN\_HORIZONTAL\_SHEET\_FEED\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-min-horizontal-sheet-feed-size)

[**WIA\_DPS\_MIN\_VERTICAL\_SHEET\_FEED\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-min-vertical-sheet-feed-size)

[**WIA\_DPS\_PAGES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-pages)

[**WIA\_DPS\_表\_送纸器\_注册**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-sheet-feeder-registration)

[**WIA\_DPS\_VERTICAL\_SHEET\_FEED\_SIZE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-vertical-sheet-feed-size)

### <a name="properties-on-transparency-scanner-root-items-windows-xp-and-windows-me"></a>透明度扫描程序的属性根项 (Windows XP 和 Windows Me)

WIA 微型驱动程序提供以下属性：

[**WIA\_DPS\_透明度**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-transparency)

[**WIA\_DPS\_TRANSPARENCY\_SELECT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-transparency-select)

 

 




