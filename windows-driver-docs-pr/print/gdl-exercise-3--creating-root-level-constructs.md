---
title: GDL 练习 3 创建根级别构造
description: GDL 练习 3 创建根级别构造
ms.assetid: 3c7ad284-b77c-4ad3-8334-2fe5b026e340
keywords:
- GDL WDK 示例
- 示例 WDK GDL
- 教程 WDK GDL
- GDL WDK 教程
- 构造 WDK GDL，创建构造
- 创建 GDL 构造 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acd075821593522ea53e5aefc061c59afb183815
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526234"
---
# <a name="gdl-exercise-3-creating-root-level-constructs"></a>GDL 练习 3:创建根级别构造


### <a href="" id="exercise"></a> 练习

修改的架构[练习 1](gdl-exercise-1--implementing-a-gdl-schema.md)引入名为的构造\*PFeature 可以仅在根级别找到的。

使用以下条件：

-   \*PFeature 可以具有任何实例的名称。

-   \*PFeature 成员是名为的属性**\*名称**并 **\*DefaultOption**。

-   \*PFeature 具有一个名为构造成员 **\*Poption** ，应声明为虚拟的。

### <a href="" id="solution"></a> 解决方案

以下模板满足上述条件。

```cpp
*Template:  POPTION
{
    *Name:  "*POption"
    *Type: CONSTRUCT
    *Virtual:  TRUE
}

*Template:  NAME
{
    *Name:  "*Name"
    *Type:  ATTRIBUTE
    *ValueType:  NORMAL_STRING
}

*Template:  SYMBOL
{
    *Type:  DATATYPE
    *DataType:   FILTER_TYPE
    *ElementType:  XML_STRING
    *FilterTypeName: "SYMBOLNAME"
}
*Template:  DEFAULT_OPT
{
    *Name: "*DefaultOption"
    *Type:  ATTRIBUTE
    *ValueType:  SYMBOL
}

*Template:  PFEATURE 
{
    *Name:  "*PFeature"
    *Type: CONSTRUCT
    *Members:  (POPTION, NAME, DEFAULT_OPT)
    *Instances:  <ANY>
}
*Template:  ROOT2
{
    *Inherits: ROOT
    *Members:  (PFEATURE)
}
```

 

 




