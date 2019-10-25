---
title: 基于 GPD/PPD 的功能说明更改
description: 基于 GPD/PPD 的功能说明更改
ms.assetid: 22333d78-f78f-4031-a9f3-50b43ec746b6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b9ccbab27fefb9eeca0a433e47a01e8b3b891fa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844582"
---
# <a name="gpdppd-based-feature-description-changes"></a>基于 GPD/PPD 的功能说明更改


Microsoft XPSDrv Unidrv/PScript5 驱动程序不包含任何硬编码的 Unidrv/PScript5 功能。 如果核心驱动程序配置模块需要处理功能、选项或约束，则应在 GPD 或 PPD 文件中指定每个功能、选项和约束。 你仍可以实现为非 GPD 或非 PPD 功能、选项或约束提供支持的配置插件。

根 GPD 或 PPD 文件（在 INF 文件中指定为驱动程序的数据文件）是核心驱动程序配置模块将分析的内容。 此根 GPD 或 PPD 文件可以包含其他 GPD 或 PPD 文件，以启用 GPD 或 PPD 文件的模块化设计。 除了包含

Msxpsinc gpd 和 Msxpsinc 文件，你可以决定如何为筛选器管道构造 GPD 和 PPD 文件。 建议将筛选器与 GPD 或 PPD 文件配对，以最大程度地提高筛选器的可重用性。

下面的代码示例演示了一个 GPD 示例，用于指定在基于 Unidrv 的 XPSDrv 筛选器管道中筛选器支持的反向订单打印功能：

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

在前面的示例中，"ReverseOrderPrinting" 自定义 GPD 功能是通过两个自定义选项定义的： "FrontToBack" 和 "BackToFront"。 该示例使用**PrintSchemaKeywordMap**关键字将 GPD 自定义功能或选项映射到公共打印架构关键字。

下面的代码示例演示了一个 PPD 示例，用于指定在基于 PScript5 的 XPSDrv 筛选器管道中筛选器支持的页面方向功能。

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

在前面的示例中，定义了包含三个自定义选项的自定义 PPD 功能，以指定筛选器支持三个 Print Schema standard PageOrientation 选项。

通过使用**PrintSchemaKeywordMap**或**MSPrintSchemaKeywordMap**关键字，将使用映射的公共打印架构关键字在 XML PrintCapabilities 或 printticket 中正确公开这些 GPD 或 PPD 自定义功能或选项。

在核心驱动程序的 DEVMODE 结构中，这些自定义 GPD 或 PPD 功能的设置存储在选项数组中。

**注意**   适用于 Windows 7， **MxdcGetPDEVAdjustment**函数具有用于横向旋转的新参数。 有关详细信息，请参阅[**MxdcXDCGetPDEVAdjustment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mxdc/nf-mxdc-mxdcgetpdevadjustment)。

 

## <a name="related-topics"></a>相关主题
[**MxdcXDCGetPDEVAdjustment**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mxdc/nf-mxdc-mxdcgetpdevadjustment)  
[V4 打印机驱动程序本地化](v4-driver-localization.md)  



