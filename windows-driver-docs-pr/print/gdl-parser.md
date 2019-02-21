---
title: GDL 分析器
description: GDL 分析器
ms.assetid: abb0e9b7-db98-4f8c-af15-83cd1841e5c2
keywords:
- GDL WDK 分析器
- 分析器 WDK GDL，关于
- 打印机驱动程序 WDK、 数据转换为 XML
- 将数据转换成 XML WDK GDL
- 将数据转换为 XML WDK GDL
- 分析 GDL 数据 WDK
- 快照 WDK GDL，GDL 分析器
- 分析器 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: deb6613783927531d6e86a94a013a31795e4dfda
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555156"
---
# <a name="gdl-parser"></a>GDL 分析器


GDL 分析器将 GDL 数据转换 XML 快照。 有关控制分析器的详细信息，请参阅[IPrintCoreHelperUni](details-of-the-iprintcorehelperuni-interface.md)接口。

提供了 GDL[标准分析](standard-gdl-parsing.md)并[基于模板的分析](gdl-template-structure.md)。

分析器筛选器可识别多种*数据类型的基元*。 这些数据类型可以显示为属性的值，并且映射到其最接近的 XML 等效 XML 快照中。 此外，分析器筛选器可以识别从基元数据类型创建的复合数据类型。 数据类型模板用于定义数据类型和 **\*ValueType**指令用于将数据类型模板与属性模板相关联。

有关标准分析的详细信息，请参阅[标准 GDL 分析](standard-gdl-parsing.md)。

有关模板的数据类型的详细信息，请参阅[GDL 模板数据类型](gdl-template-data-types.md)。

有关故障排除分析有关的信息，请参阅[故障排除 GDL 分析](troubleshooting-gdl-parsing.md)。

 

 




