---
title: GDL 练习 1 实现 GDL 架构
description: GDL 练习 1 实现 GDL 架构
ms.assetid: 0adfef5a-4211-45e9-bb65-8174822efdc5
keywords:
- GDL WDK 示例
- 示例 WDK GDL
- 教程 WDK GDL
- GDL WDK 教程
- WDK GDL，实现 GDL 架构的架构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19b806cbb9e93fef831741f0b4831ed9710374b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567572"
---
# <a name="gdl-exercise-1-implementing-a-gdl-schema"></a>GDL 练习 1：实现 GDL 架构


### <a href="" id="exercise"></a> 练习

实现创建三个类别的属性，并不会施加构造可以位于的限制的架构。

这些属性必须被划分为以下类别：

-   内部可以出现在根级别构造的属性。

-   只能出现在根级别的特性。

-   可以仅出现在构造的属性。

在您的架构; 未定义任何关键字只需包括将来的关键字的框架。

**请注意**  可以通过使用模板，创建虚拟架构-即，不会定义任何 GDL 条目的架构。 在这种方式中定义的基本架构施加影响的无论如何将来扩展此架构。

 

### <a href="" id="solution"></a> 解决方案

下面的代码示例演示如何完成此练习中的一种方法。

```cpp
*Template:  ATTRIBUTE
{
    *Type:  ATTRIBUTE
    *Virtual:  TRUE
}
*Template:  ROOT_ATTRIB
{
    *Inherits: ATTRIBUTE
    *Virtual:  TRUE
}
*Template:     CONSTRUCT_ATTRIB  *%  May not appear at Root level
{
    *Inherits: ATTRIBUTE
    *Virtual:  TRUE
}
*Template:     FREEFLOAT
{
    *Inherits: ATTRIBUTE
    *Virtual:  TRUE
}
*Template:  CONSTRUCTS
{
    *Type: CONSTRUCT
    *Members:  ( CONSTRUCTS, FREEFLOAT, CONSTRUCT_ATTRIB)
    *Virtual:  TRUE
}

*Template:  ROOT
{
            *Type: CONSTRUCT
            *AllowNewMembers: FALSE
            *Name:  "root"
            *Instances:  <ANY>
            *Members:  (ROOT_ATTRIB, FREEFLOAT, CONSTRUCTS)
}
```

**请注意**  您可以将模板放 MasterTemplate.gdl 文件中以使用在前面的示例中的下一个练习。

 

 

 




