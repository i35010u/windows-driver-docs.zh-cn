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
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388116"
---
# <a name="gdl-exercise-3-creating-root-level-constructs"></a>GDL 练习 3：创建根级构造


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

 

 




