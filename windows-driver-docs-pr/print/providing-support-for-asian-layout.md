---
title: 提供亚洲语言布局支持
description: 提供亚洲语言布局支持
ms.assetid: 38c7dfca-ce30-4967-84a4-e2f40bba8c57
keywords:
- 打印处理器 WDK，亚洲语言
- 亚洲语言 WDK 打印
- 手册 WDK 打印
- N 个打印 WDK
- 反向转换 WDK 打印
- 阿拉伯打印支持 WDK
- 日语打印支持 WDK
- 乌尔都语打印支持 WDK
- 国际化注意事项 WDK
- 打印亚洲语言 WDK
- 语言 WDK 打印
- 从右到左阅读语言 WDk 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50cb696a1b75f781835f95419b9e7d34374e7819
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840420"
---
# <a name="providing-support-for-asian-layout"></a>提供亚洲语言布局支持


Microsoft Windows 打印处理器支持从右到左阅读的亚洲语言，如阿拉伯语、日语和乌尔都语，具有以下功能：

-   **N 向上方向**：在单张纸上打印多页时，用户可以按从右到左的顺序在工作表上打印页面。

-   **手册边缘**：打印小册子，其中折叠了页面并并排布局页面，用户可以从右到左排列页面。 下图显示了使用手册\_边缘\_右标志的手册的页面布局。使用手册\-边缘\-右标志说明手册的页面布局![关系图](images/asian-booklet.png)

在 Windows Vista 中，可以使用标志更改驱动程序中的 N 向上方向和手册边缘以支持亚洲布局。 有关如何设置这些值的详细信息，请参阅[**DrvQueryJobAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvqueryjobattributes) and [**ATTRIBUTE\_INFO\_4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/ns-winddiui-_attribute_info_4)。

 

 




