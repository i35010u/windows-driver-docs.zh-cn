---
title: GDL 值
description: GDL 值
keywords:
- GDL WDK，值
- 值 WDK GDL，关于 GDL 值
- 值 WDK GDL，个字符
- GDL WDK，上下文
- GDL WDK，值宏引用
- 值宏引用 WDK GDL
- 值 WDK GDL，示例
- 上下文 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4d80b1a6985e46b43a507af5664ce562564691e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796911"
---
# <a name="gdl-values"></a>GDL 值


*GDL 值* 是一个字符串，该字符串以冒号分隔符后找到的 GDL 属性中的第一个非空白字符开头，并在达到 linebreak 序列或构造分隔符时通常结束。

当 linebreak 序列或构造分隔符不终止值时，有几个 [GDL 上下文](gdl-contexts.md) 。 这些特殊的上下文包括：

-   构造分隔符字符作为注释的一部分出现。

-   终止字符作为带引号的字符串的一部分出现。

-   终止字符出现在 [嵌套上下文](gdl-nested-contexts.md)中。

-   终止字符出现在 [任意值](gdl-arbitrary-value-contexts.md)中。

值可以包含零个、一个或多个特殊的上下文。 单个上下文类型可以在一个值中多次出现。 前面的任何特定上下文也可能出现在任何其他上下文的外部。 某些上下文可能出现在另一个上下文中;每个上下文的说明中注明了这些情况。 必须先退出所有上下文，然后才能通过 linebreak 序列或构造分隔符终止值。

终止 linebreak 序列或构造分隔符不被视为值的一部分。

值在 [GDL 属性](gdl-attributes.md)中是可选的。

*值宏引用* 可能出现在允许非文本空白的 GDL 值中的任何位置;这些引用以等号 (=) 开头。 当在此类上下文中使用等号而不打算引入值宏引用时，等号后面必须跟一个非符号字符 (如空白) 。 有关值宏的详细信息，请参阅 [GDL 值 macros](gdl-value-macros.md)。

有关 GDL 上下文的详细信息，请参阅 [GDL 上下文](gdl-contexts.md)。

下面的代码示例显示 GDL 分析器可接受的值。

```cpp
*Value: *%  Null Value - only a comment

*Value: "Quoted String"

*Value: "Quoted String with Hex substring: <48 65 78> see?"

*Value: "Hex substring with comment and macro reference <48 *% comment
65 78 =MacroRef > see?"   *% note continuation linebreak was automatically assumed

*Value: tokens (parenthesis context) [followed by square brackets context] "ending in quoted string"

*Value: tokens (parenthesis context {with nested curly braces context})

*Value:  tokens <BeginValue:anything> no special characters or contexts recognized within an arbitrary value context.  " } ) * % < > anything goes, sorry  =MacroRefs not recognized
*Keyword:  looks like a new entry but its still within the Arbitrary Value context.
+  not continuation chars, *% this is not a comment  <EndValue:anything>
```

 

 




