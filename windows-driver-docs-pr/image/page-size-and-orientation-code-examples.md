---
title: 页面大小和方向代码示例
description: 页面大小和方向代码示例
ms.assetid: 28425df2-131b-4fbc-ae44-043be2fb4813
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c39b7c11caa240d8812b4cf3be5946c448e8f1d8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192601"
---
# <a name="page-size-and-orientation-code-examples"></a>页面大小和方向代码示例

这些代码示例显示了以下 WIA \_ ip \_ 页面 \_ 大小方案：

1.  微型驱动程序报告设置。

2.  应用程序将 "WIA \_ ip \_ 页面 \_ 大小" 属性设置为 "wia \_ 页面 \_ 字母"。

3.  应用程序将 " [**WIA \_ ip \_ 方向**](./wia-ips-orientation.md) " 属性设置为 "LANSCAPE"。

4.  应用程序会将 [**WIA \_ IPS \_ XEXTENT**](./wia-ips-xextent.md) 属性更改为较小的值。

### <a name="example-1-the-minidriver-reports-the-settings"></a>示例1：微型驱动程序报告设置

在下面的代码示例中，微型驱动程序在应用程序设置任何 WIA 属性之前设置自定义选择区域。 在这种情况下，选择区域表示整个平台。

WIA_IPS_PAGE_SIZE = WIA_PAGE_CUSTOM WIA_IPS_PAGE_WIDTH = 11500 WIA_IPS_PAGE_HEIGHT = 14000 WIA_IPS_ORIENTATION = 纵向 WIA_IPS_XPOS = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 1150 WIA_IPS_YEXTENT = 1400 WIA_IPS_XRES = 100 WIA_IPS_YRES = 100

### <a name="example-2-an-application-sets-the-wia_ips_page_size-property-to-wia_page_letter"></a>示例2：应用程序将 "WIA \_ ip \_ 页面 \_ 大小" 属性设置为 "wia" \_ 页面 \_ 字母

在下面的代码示例中，微型驱动程序将页面大小从自定义值更改为8500×11000像素的标准字母大小。

WIA_IPS_PAGE_SIZE = WIA_PAGE_LETTER WIA_IPS_PAGE_WIDTH = 8500 WIA_IPS_PAGE_HEIGHT = 11000 WIA_IPS_ORIENTATION = 纵向 WIA_IPS_XPOS = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 850 WIA_IPS_YEXTENT = 1100 WIA_IPS_XRES = 100 WIA_IPS_YRES = 100

### <a name="example-3-an-application-sets-the-wia_ips_orientation-property-to-lanscape"></a>示例3：应用程序将 WIA \_ ip \_ 方向属性设置为 LANSCAPE

在下面的代码示例中，微型驱动程序将页面方向从纵向更改为横向。 物理平台必须能够获取最初处于横向方向的页面。

WIA_IPS_PAGE_SIZE = WIA_PAGE_LETTER WIA_IPS_PAGE_HEIGHT = 11000 WIA_IPS_PAGE_WIDTH = 8500 WIA_IPS_ORIENTATION = LANSCAPE WIA_IPS_XPOS = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 1100 WIA_IPS_YEXTENT = 850 WIA_IPS_XRES = 100 WIA_IPS_YRES = 100

### <a name="example-4-an-application-changes-the-wia_ips_xextent-property-to-a-smaller-value"></a>示例4：应用程序将 WIA \_ IPS \_ XEXTENT 属性更改为较小的值

在下面的代码示例中，应用程序将 [**WIA \_ IPS \_ XEXTENT**](./wia-ips-xextent.md) 属性更改为1000。 微型驱动程序应假设 WIA ips XEXTENT 中包含的新值 \_ \_ 对于 "wia \_ ip \_ 页面大小" 属性不再有效 \_ ，因此应将 wia \_ IP \_ 页面 \_ 大小更改为 "wia \_ 页面 \_ 自定义"。 微型驱动程序还必须调整 [**WIA \_ ip \_ 页面 \_ 宽度**](./wia-ips-page-width.md)。

WIA_IPS_PAGE_SIZE = WIA_PAGE_CUSTOM WIA_IPS_PAGE_HEIGHT = 10000 WIA_IPS_PAGE_WIDTH = 8500 WIA_IPS_ORIENTATION = LANSCAPE WIA_IPS_XPOS = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 1000 WIA_IPS_YEXTENT = 850 WIA_IPS_XRES = 100 WIA_IPS_YRES = 100