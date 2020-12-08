---
title: GDL 构造
description: GDL 构造
keywords:
- GDL WDK、构造
- 构造 WDK GDL
- 子条目 WDK GDL
- 父构造 WDK GDL
- 祖先构造 WDK GDL
- 语法构造 WDK GDL
- 逻辑构造 WDK GDL
- 联合 WDK GDL
- 构造 WDK GDL、语法构造
- 构造 WDK GDL，逻辑构造
- 构造 WDK GDL，联合
- 构造 WDK GDL，分隔符
- 构造 WDK GDL，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68a75e91f3676f9a6a6f12bc653ab80b4405329b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797029"
---
# <a name="gdl-constructs"></a>GDL 构造


*GDL 构造* 只是一个 [GDL 属性](gdl-attributes.md)，后跟构造主体。 从逻辑上讲，构造表示数据的集合，这与 C 结构非常类似。

*构造体* 为零个、一个或多个 GDL 条目，其中包含 [构造分隔符字符](gdl-construct-delimiters.md)。 构造体必须由左大括号引入 ( {) ，并由右大括号 (} ) 终止。

由构造分隔符字符括起来的 GDL 项称为构造的 *内容* 。 包含的 GDL 项也称为子元素 *、**子**元素、子元素* 或构造 *成员*。 因为子条目也可以是构造，所以可以创建任意深度的构造 nestings;但是，只会将父构造的直接后代称为 *子条目*。

相反，直接包含子项的构造有时称为 *父构造*。 共享同一父构造的两个 GDL 条目称为 *同级*。 一个结构，其正文包含某个条目的父项或某个条目的父项 (以此类推，依此类推) 称为 *祖先构造*。

构造主体之前的属性称为 *构造头*，有时只是 *构造*。 构造头的关键字组件称为 *构造类型*。 如果定义了多个同级构造，其中每个同级构造都具有相同的关键字，则它们被视为属于相同的构造类型。 构造头的值组成部分称为 *构造实例名称* 或 *构造标记*。 构造标记应为 [符号](gdl-arbitrary-value-contexts.md)。 构造标记在语法上是可选的，但在某些情况下是必需的。

构造可以是 *句法* 或 *逻辑*。 构造可以包含联合。

任意数量的空格和 linebreak 序列都可以位于 [构造分隔符字符](gdl-construct-delimiters.md)之前或之后。 但是，为了便于阅读，通常使用 C 样式缩进约定。

下面的代码示例演示了 GDL 构造。

```cpp
*ConstructType: ConstructTag
{   *%  Begin Construct Delimiter
*%  this is the Construct Body
*ChildAttribute: child attribute value
*ChildConstruct: ChildConstructTag
{
 *%  Body of Child construct could hold more constructs.
}
*AnotherChildConstruct: ChildConstructTag2
{
 *% Contents of *AnotherChildConstruct
 *% since both child constructs share the same Parent construct, they are
 *% Sibling Constructs.
 *DescendantAttribute:  this attribute is a descendant of  *ConstructType: ConstructTag
}
}   *%  End Construct Delimiter
```

本节包括：

[GDL 构造分隔符](gdl-construct-delimiters.md)

[GDL 中的语法和逻辑构造](syntactical-and-logical-constructs-in-gdl.md)

[GDL 构造联合](gdl-construct-unions.md)

[GDL 空白字符](gdl-whitespace-characters.md)

[GDL 注释](gdl-comments.md)

[GDL 字符串](gdl-strings.md)

 

 




