---
title: GDL 模板
description: GDL 模板
ms.assetid: 9cce885d-395e-4f8d-8076-951d75d82410
keywords:
- GDL WDK 模板
- 模板 WDK GDL
- 验证 GDL 条目 WDK GDL
- GDL WDK，验证条目
- 在模板中的 WDK GDL 属性
- 模板中的构造 WDK GDL
- 继承 WDK GDL
- WDK GDL，基于继承的架构的架构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0e61d5c5b20dc6c72f9103f0ad5ff8b29e20fe3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329683"
---
# <a name="gdl-templates"></a>GDL 模板


*GDL 模板*为分析器验证 GDL 条目提供的方法。 每个条目可以与特定的模板相关联。

GDL 提供可以通过添加新的模板扩展的标准模板。 标准模板定义的所有[特性](gdl-attributes.md)并[构造](gdl-constructs.md)已知到操作系统。

定义模板之间的关系[继承](gdl-template-inheritance.md)。

GDL 分析器将 GDL 文件中的每个数据条目与模板相关联。 如果数据输入是一种构造，该模板指定以间接方式的所有成员可以出现在该构造。 此关联是以递归方式应用，以便每个数据条目可以有与之关联的模板。 模板使用特定[条件](criteria-for-associating-gdl-templates-with-keywords.md)来定义模板如何相关的数据和特定[数据类型](gdl-template-data-types.md)用于模板。

使用特定 GDL[指令](gdl-template-directives.md)模板。

 

 




