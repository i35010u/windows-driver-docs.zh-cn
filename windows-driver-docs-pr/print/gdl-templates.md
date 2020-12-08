---
title: GDL 模板
description: GDL 模板
keywords:
- GDL WDK，模板
- 模板 WDK GDL
- 验证 GDL 条目 WDK GDL
- GDL WDK，验证条目
- 属性中的 WDK GDL
- 在模板中构造 WDK GDL
- 继承 WDK GDL
- 架构 WDK GDL，基于继承的架构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eef3c32e4437515b2c25c4bfef05cb2c8b4c0fb4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835899"
---
# <a name="gdl-templates"></a>GDL 模板


*GDL 模板* 为分析器提供验证 GDL 条目的方法。 每个条目均可与特定模板关联。

GDL 提供可通过添加新模板来扩展的标准模板。 标准模板定义操作系统已知的所有 [属性](gdl-attributes.md) 和 [构造](gdl-constructs.md) 。

模板之间的关系由 [继承](gdl-template-inheritance.md)定义。

GDL 分析器将 GDL 文件中的每个数据条目与一个模板关联。 如果数据输入为构造，则模板以间接方式指定可在该构造内显示的所有成员。 此关联以递归方式应用，以便每个数据输入都可以有与之关联的模板。 模板使用特定的 [条件](criteria-for-associating-gdl-templates-with-keywords.md) 来定义模板与数据的关联方式，并使用特定的 [数据类型](gdl-template-data-types.md) 来用于模板。

GDL 对模板使用特定 [指令](gdl-template-directives.md) 。

 

 




