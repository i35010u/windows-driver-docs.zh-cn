---
title: GDL 练习3创建 Root-Level 构造
description: GDL 练习3创建 Root-Level 构造
keywords:
- GDL WDK，示例
- 示例 WDK GDL
- 教程 WDK GDL
- GDL WDK，教程
- 构造 WDK GDL，创建构造
- 创建 GDL 构造 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d802b7f709d1ed695764fa923598a00c89ea95e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835977"
---
# <a name="gdl-exercise-3-creating-root-level-constructs"></a>GDL 练习3：创建 Root-Level 构造


### <a name="exercise"></a><a href="" id="exercise"></a> 小心谨慎

修改 [练习 1](gdl-exercise-1--implementing-a-gdl-schema.md) 的架构，引入一个名为 \* PFeature 的构造，该构造只能在根级别找到。

使用以下条件：

-   \*PFeature 可以具有任何实例名称。

-   \*PFeature 成员是名为 **\* Name** 和 **\* DefaultOption** 的属性。

-   \*PFeature 有一个名为 **\* Poption** 的构造成员，该成员应声明为 virtual。

### <a name="solution"></a><a href="" id="solution"></a> 解决方案

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

 

 




