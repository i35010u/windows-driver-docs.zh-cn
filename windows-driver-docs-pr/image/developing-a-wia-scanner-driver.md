---
title: 开发 WIA 扫描仪驱动程序
description: 开发 WIA 扫描仪驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46e7c8124906f96085d493ceafa3491e8fc9740a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792895"
---
# <a name="developing-a-wia-scanner-driver"></a>开发 WIA 扫描仪驱动程序





WIA 扫描器驱动程序开发人员可以创建 WIA microdriver 或 WIA 微型驱动程序。

### <a name="microdriver"></a>Microdriver

Microdriver 是支持简单平板扫描仪的小型驱动程序。 此驱动程序类型的开发速度比微型驱动程序更快，但具有以下限制：

-   Microdrivers 仅限于平板扫描仪。

-   Microdrivers 仅提供最少的文档送纸器支持 (不) 双工操作。

-   Microdrivers 提供有限数量的分辨率（以每英寸点数为单位） (dpi) ：75、100、150、200、300和600。

-   Microdrivers 仅支持 WiaImgFmt \_ BMP 和 WiaImgFmt \_ MEMORYBMP 图像格式。 有关这些图像格式的详细信息，请参阅 Microsoft Windows SDK。

-   Microdrivers 不支持较早的颜色扫描器使用三通扫描 (来) 使用颜色筛选器捕获颜色图像。

有关开发 microdrivers 的详细信息，请参阅 [创建 WIA Microdriver](creating-a-wia-microdriver.md)。

### <a name="minidriver"></a>微型驱动程序

微型驱动程序是完整的 WIA 微型驱动程序。 有关详细信息，请参阅 [创建 WIA 微型驱动程序](creating-a-wia-minidriver.md) 部分。

本部分包含有关以下主题的其他信息：

[WIA 扫描仪项树布局](wia-scanner-item-tree-layout.md)

[添加文档送纸器支持](adding-document-feeder-support.md)

[页面大小和方向](page-size-and-orientation.md)

[TWAIN 兼容性](twain-compatibility.md)

 

 




