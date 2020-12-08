---
title: GDL 分析器
description: GDL 分析器
keywords:
- GDL WDK，分析器
- 分析器 WDK GDL，关于
- 打印机驱动程序 WDK，将数据转换为 XML
- 将数据转换为 XML WDK GDL
- 将数据转换为 XML WDK GDL
- 分析 GDL 数据 WDK
- 快照 WDK GDL，GDL 分析器
- 分析器 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc41dd6b956b7f1bbf949308f7d0274d0f8d509c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796975"
---
# <a name="gdl-parser"></a>GDL 分析器


GDL 分析器将 GDL 数据转换为 XML 快照。 有关控制分析器的详细信息，请参阅 [IPrintCoreHelperUni](details-of-the-iprintcorehelperuni-interface.md) interface。

GDL 提供 [标准分析](standard-gdl-parsing.md) 和 [基于模板的分析](gdl-template-structure.md)。

分析器筛选器可识别各种 *数据类型基元*。 这些数据类型可以显示为属性的值，并在 XML 快照中映射到其最接近的 XML 等效值。 此外，分析器筛选器可识别从基元数据类型创建的复合数据类型。 数据类型模板用于定义数据类型，而 **\* ValueType** 指令用于将数据类型模板与属性模板相关联。

有关标准分析的详细信息，请参阅 [标准 GDL 分析](standard-gdl-parsing.md)。

有关模板数据类型的详细信息，请参阅 [GDL Template Data types](gdl-template-data-types.md)。

有关分析的疑难解答信息，请参阅 [GDL 分析故障排除](troubleshooting-gdl-parsing.md)。

 

 




