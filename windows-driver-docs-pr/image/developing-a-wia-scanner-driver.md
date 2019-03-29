---
title: 开发 WIA 扫描仪驱动程序
description: 开发 WIA 扫描仪驱动程序
ms.assetid: befe7e36-cb42-48da-88b4-d8983876266f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 624fb0ee5f3755e4dcb115b5995fc92717c381eb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569428"
---
# <a name="developing-a-wia-scanner-driver"></a>开发 WIA 扫描仪驱动程序





WIA 扫描程序驱动程序开发人员可以创建 WIA microdriver 或 WIA 微型驱动程序。

### <a name="microdriver"></a>Microdriver

Microdriver 是一个小的驱动程序支持简单平板扫描仪。 此驱动程序类型可以比微型驱动程序，更快地开发，但有以下限制：

-   Microdrivers 被限制为仅平板扫描仪。

-   Microdrivers 只提供最少文档送纸器的支持 （没有双工操作）。

-   Microdrivers 提供有限的数量的每英寸点数 (dpi) 中的解决方法：75、 100、 150，200，300 和 600。

-   Microdrivers 支持仅 WiaImgFmt\_BMP 和 WiaImgFmt\_MEMORYBMP 图像格式。 有关这些图像格式的详细信息，请参阅 Microsoft Windows SDK。

-   Microdrivers 不支持三个传递扫描 （使用旧颜色扫描仪捕获使用颜色筛选器的颜色映像）。

有关开发 microdrivers 的详细信息，请参阅[创建 WIA Microdriver](creating-a-wia-microdriver.md)。

### <a name="minidriver"></a>微型驱动程序

微型驱动程序是完整的 WIA 微型驱动程序。 请参阅[创建 WIA 微型驱动程序](creating-a-wia-minidriver.md)部分，了解详细信息。

本部分包含有关以下主题的其他信息：

[WIA 扫描程序项树布局](wia-scanner-item-tree-layout.md)

[添加文档送纸器支持](adding-document-feeder-support.md)

[页大小和方向](page-size-and-orientation.md)

[TWAIN 兼容性](twain-compatibility.md)

 

 




