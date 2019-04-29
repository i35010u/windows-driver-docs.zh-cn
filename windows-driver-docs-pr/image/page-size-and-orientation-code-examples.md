---
title: 页面大小和方向代码示例
description: 页面大小和方向代码示例
ms.assetid: 28425df2-131b-4fbc-ae44-043be2fb4813
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51b1f49c74815c249ef98eed60fa5f2acc325a17
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392623"
---
# <a name="page-size-and-orientation-code-examples"></a>页面大小和方向代码示例

这些代码示例显示以下 WIA\_IPS\_页\_大小方案：

1.  微型驱动程序报告的设置。

2.  应用程序设置 WIA\_IPS\_页面\_大小属性设置为 WIA\_页\_字母。

3.  应用程序设置[ **WIA\_IPS\_方向**](https://msdn.microsoft.com/library/windows/hardware/ff552625) LANSCAPE 属性。

4.  应用程序更改[ **WIA\_IPS\_大 XEXTENT** ](https://msdn.microsoft.com/library/windows/hardware/ff552661)属性设置为较小的值。

### <a name="example-1-the-minidriver-reports-the-settings"></a>示例 1：微型驱动程序报告的设置

在下面的代码示例中，微型驱动程序之前应用程序设置任何 WIA 属性设置自定义选择区域。 在这种情况下，选择区域表示整个平板。

WIA_IPS_PAGE_SIZE = WIA_PAGE_CUSTOM WIA_IPS_PAGE_WIDTH = 11500 WIA_IPS_PAGE_HEIGHT = 14000 WIA_IPS_ORIENTATION = 纵向 WIA_IPS_XPOS = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 1150 WIA_IPS_YEXTENT = 1400 WIA_IPS_XRES = 100 WIA_IPS_YRES = 100

### <a name="example-2-an-application-sets-the-wiaipspagesize-property-to-wiapageletter"></a>示例 2：应用程序设置 WIA\_IPS\_页面\_大小属性设置为 WIA\_页\_字母

在下面的代码示例，微型驱动程序更改页面大小为 8500 × 11000 像素为单位的标准字母大小从自定义值中。

WIA_IPS_PAGE_SIZE = WIA_PAGE_LETTER WIA_IPS_PAGE_WIDTH = 8500 WIA_IPS_PAGE_HEIGHT = 11000 WIA_IPS_ORIENTATION = 纵向 WIA_IPS_XPOS = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 850 WIA_IPS_YEXTENT = 1100 WIA_IPS_XRES = 100 WIA_IPS_YRES = 100

### <a name="example-3-an-application-sets-the-wiaipsorientation-property-to-lanscape"></a>示例 3：应用程序设置 WIA\_IP\_LANSCAPE 方向属性

在下面的代码示例，微型驱动程序从纵向向横向更改页面方向。 物理平台必须能够获取最初在横向方向的页面。

WIA_IPS_PAGE_SIZE = WIA_PAGE_LETTER WIA_IPS_PAGE_HEIGHT = 11000 WIA_IPS_PAGE_WIDTH = 8500 WIA_IPS_ORIENTATION = LANSCAPE WIA_IPS_XPOS = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 1100 WIA_IPS_YEXTENT = 850 WIA_IPS_XRES = 100 WIA_IPS_YRES = 100

### <a name="example-4-an-application-changes-the-wiaipsxextent-property-to-a-smaller-value"></a>示例 4：应用程序更改 WIA\_IP\_大 XEXTENT 属性设置为较小的值

在下面的代码示例中，应用程序更改[ **WIA\_IPS\_大 XEXTENT** ](https://msdn.microsoft.com/library/windows/hardware/ff552661)属性设置为 1000年。 微型驱动程序应假定，新值，该值包含在 WIA\_IPS\_大 XEXTENT 不再有效的 WIA\_IPS\_页\_SIZE 属性，从而应更改 WIA\_IP\_页上\_WIA 的大小\_页面\_自定义。 微型驱动程序还必须调整[ **WIA\_IPS\_页\_宽度**](https://msdn.microsoft.com/library/windows/hardware/ff552636)。

WIA_IPS_PAGE_SIZE = WIA_PAGE_CUSTOM WIA_IPS_PAGE_HEIGHT = 10000 WIA_IPS_PAGE_WIDTH = 8500 WIA_IPS_ORIENTATION = LANSCAPE WIA_IPS_XPOS = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 1000 WIA_IPS_YEXTENT = 850 WIA_IPS_XRES = 100 WIA_IPS_YRES = 100
