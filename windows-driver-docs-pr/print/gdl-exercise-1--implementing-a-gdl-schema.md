---
title: GDL 练习1实现 GDL 架构
description: GDL 练习1实现 GDL 架构
keywords:
- GDL WDK，示例
- 示例 WDK GDL
- 教程 WDK GDL
- GDL WDK，教程
- 架构 WDK GDL，实现 GDL 架构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 972acd6924185945cd99f3e8e0390df207265838
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835979"
---
# <a name="gdl-exercise-1-implementing-a-gdl-schema"></a>GDL 练习1：实现 GDL 架构


### <a name="exercise"></a><a href="" id="exercise"></a> 小心谨慎

实现一个架构，该架构创建三个类别的属性，不对可以定位构造的位置施加限制。

这些属性必须分为以下几类：

-   可在根级别和构造内出现的特性。

-   只能在根级别出现的特性。

-   只能出现在构造中的特性。

不要在架构中定义任何关键字;只需为将来的关键字包括框架。

**注意**   通过使用模板，你可以创建虚拟架构，即未定义任何 GDL 条目的架构。 以这种方式定义的基本架构对其影响，而不考虑未来如何扩展此架构。

 

### <a name="solution"></a><a href="" id="solution"></a> 解决方案

下面的代码示例演示了完成此练习的一种方法。

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

**注意**   您可以将上述示例中的模板放置在 MasterTemplate. gdl 文件中，以便在下一练习中使用。

 

 

 




