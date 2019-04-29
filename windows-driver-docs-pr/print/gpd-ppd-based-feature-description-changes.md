---
title: 基于 GPD/PPD 的功能说明更改
description: 基于 GPD/PPD 的功能说明更改
ms.assetid: 22333d78-f78f-4031-a9f3-50b43ec746b6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd016a303f82016e5c9ba9453223c15585675717
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385181"
---
# <a name="gpdppd-based-feature-description-changes"></a>基于 GPD/PPD 的功能说明更改


Microsoft XPSDrv Unidrv/PScript5 驱动程序不包含任何硬编码 Unidrv/PScript5 功能。 您应 GPD 或 PPD 文件中指定每个功能、 选项和约束如果核心驱动程序配置模块需要处理功能、 选项或约束。 你仍然可以实现配置插件为非 GPD 或非 PPD 功能、 选项或约束提供支持。

（这与驱动程序的数据文件的 INF 文件中指定） 的根 GPD 或 PPD 文件是核心驱动程序配置模块将分析。 此根 GPD 或 PPD 文件可以包含其他 GPD 或 PPD 文件，若要启用 GPD 或 PPD 文件的模块化设计。 除了包含

Msxpsinc.gpd 和 Msxpsinc.ppd 文件，可以决定如何构造筛选器管道的 GPD 和 PPD 文件。 我们建议你与 GPD 或 PPD 文件最大限度地筛选器的可重用性配对您的筛选器。

下面的代码示例显示一个 GPD 示例来指定筛选器支持在基于 Unidrv XPSDrv 筛选器管道中的反向顺序打印功能：

```cpp
*Feature: ReverseOrderPrinting
 {
 *PrintSchemaKeywordMap: "JobPageOrder"

 *Option: FrontToBack
 {
 *PrintSchemaKeywordMap: "Standard"
 }

 *Option: BackToFront
 {
 *PrintSchemaKeywordMap: "Reverse"
 }
}
```

在前面的示例中，使用两个自定义选项定义"ReverseOrderPrinting"自定义 GPD 功能："FrontToBack"和"BackToFront"。 该示例使用**PrintSchemaKeywordMap**关键字 GPD 自定义功能或选项映射到公共打印架构关键字。

下面的代码示例显示了 PPD 示例，以指定筛选器支持在 PScript5 基于 XPSDrv 筛选器管道中的页面方向功能。

```cpp
*OpenUI *PageOrientation: PickOne
*DefaultPageOrientation: Portrait
*PageOrientation Portrait: ""
*PageOrientation Landscape: ""
*PageOrientation RotatedLandscape: ""
*CloseUI: *PageOrientation

*MSPrintSchemaKeywordMap: PageOrientation  *PageOrientation
*MSPrintSchemaKeywordMap: PageOrientation Portrait *PageOrientation Portrait
*MSPrintSchemaKeywordMap: PageOrientation Landscape *PageOrientation Landscape
*MSPrintSchemaKeywordMap: PageOrientation ReverseLandscape *PageOrientation RotatedLandscape
```

在前面的示例中，定义自定义 PPD 功能包含三个自定义选项来指定支持的三个打印架构标准 PageOrientation 选项筛选器的功能。

通过使用**PrintSchemaKeywordMap**或**MSPrintSchemaKeywordMap**关键字、 这些 GPD 或 PPD 自定义功能或选项可能会正确显示在 XML PrintCapabilities 或 Printticket 使用映射公共打印架构关键字。

在核心驱动程序的 DEVMODE 结构中，这些自定义的 GPD 或 PPD 功能的设置存储选项数组中。

**请注意**  适用于 Windows 7， **MxdcGetPDEVAdjustment**函数具有横向旋转的新参数。 有关详细信息，请参阅[ **MxdcXDCGetPDEVAdjustment**](https://msdn.microsoft.com/library/windows/hardware/ff557558)。

 

## <a name="related-topics"></a>相关主题
[**MxdcXDCGetPDEVAdjustment**](https://msdn.microsoft.com/library/windows/hardware/ff557558)  
[V4 打印机驱动程序本地化](v4-driver-localization.md)  



