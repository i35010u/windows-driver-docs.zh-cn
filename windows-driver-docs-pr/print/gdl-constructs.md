---
title: GDL 构造
description: GDL 构造
ms.assetid: e579bff0-4e28-4e9e-bef2-f6748c3849e5
keywords:
- GDL WDK 构造
- 构造 WDK GDL
- 子项 WDK GDL
- 父构造 WDK GDL
- 上级构造 WDK GDL
- 语法构造 WDK GDL
- 逻辑构造 WDK GDL
- 联合 WDK GDL
- 构造 WDK GDL，语法构造
- 构造 WDK GDL，逻辑构造
- 构造 WDK GDL，联合
- 构造 WDK GDL，分隔符
- 构造 WDK GDL，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f76133493223329997f5b5cfa0befcc1d4d23870
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576517"
---
# <a name="gdl-constructs"></a>GDL 构造


一个*GDL 构造*是只需[GDL 属性](gdl-attributes.md)跟构造正文中。 在逻辑上，一种构造表示集合的数据，更类似 C 结构执行的操作。

一个*构造正文*为零、 一个或多个 GDL 条目括[构造分隔符字符](gdl-construct-delimiters.md)。 构造正文必须引入的左大括号 （{}），并终止右大括号 （}）。

由构造分隔符字符括起来的 GDL 条目嘿 *内容*构造。 括住的 GDL 条目也称为*子级*，*子项*，*子元素*，或者*成员*构造。 由于这些子项也可以是构造，你可以创建任意深度嵌套构造;但是，调用父构造中的，仅直接后代*子项*。

相反，直接包围的子项的构造有时称作*父构造*。 两个共享同一父构造的 GDL 条目被称为*同级*。 调用其正文中包含的项的父项或某项的父级的父级 （依此类推） 的构造*祖先构造*。

位于构造主体之前该属性称为*构造 head*，或有时仅*构造*。 构造 head 的关键字组件称为*构造类型*。 如果定义了多个同级构造，每个使用相同的关键字，它们被视为属于相同的构造类型。 构造头的值组件称为*构造实例名称*，或*构造标记*。 应为构造标记[符号](gdl-arbitrary-value-contexts.md)。 构造标记是可选的语法，但在某些情况下所需。

构造可以是*语法*或*逻辑*。 联合可以包含构造。

任意数量的空格和 linebreak 序列可以前面或后面[构造分隔符字符](gdl-construct-delimiters.md)。 但是，为了便于阅读，通常使用的是 C 样式缩进约定。

下面的代码示例显示了 GDL 构造。

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

本部分包括：

[GDL 构造分隔符](gdl-construct-delimiters.md)

[中 GDL 语法和逻辑的构造](syntactical-and-logical-constructs-in-gdl.md)

[GDL 构造联合](gdl-construct-unions.md)

[GDL 空白字符](gdl-whitespace-characters.md)

[GDL 注释](gdl-comments.md)

[GDL 字符串](gdl-strings.md)

 

 




