---
title: GDL 值
description: GDL 值
ms.assetid: 0e634646-d334-4b9c-b9d2-36026f617575
keywords:
- GDL WDK 值
- 有关 GDL 值 WDK GDL 值
- WDK GDL，字符的值
- GDL WDK 上下文
- GDL WDK，值宏引用
- 值宏引用 WDK GDL
- 值 WDK GDL，示例
- 上下文 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9f785d9bffeba2ec6746b39d9de9f60626bdc38
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555184"
---
# <a name="gdl-values"></a>GDL 值


一个*GDL 值*是开头的冒号分隔符之后找到和通常结束时 linebreak 序列 GDL 属性中的第一个非空白字符的字符串或达到构造分隔符。

有几个[GDL 上下文](gdl-contexts.md)时 linebreak 序列或构造分隔符不会终止值。 这些特殊的上下文包括时：

-   构造分隔符字符出现一条注释的一部分。

-   作为带引号的字符串的一部分出现终止字符。

-   终止字符中会出现[嵌入的上下文](gdl-nested-contexts.md)。

-   终止字符中会出现[任意值](gdl-arbitrary-value-contexts.md)。

值可以包含零、 一个或多个这些特殊的上下文。 单一上下文类型可以出现多次，在一个值。 任何前面的特殊上下文也会出现之外的任何其他上下文。 某些上下文中可能会出现在另一个上下文;说明每个上下文中注明了这些情况。 必须先退出所有上下文 linebreak 序列或构造分隔符可以终止值。

终止 linebreak 序列或构造分隔符是不被视为值的一部分。

值都是可选中[GDL 属性](gdl-attributes.md)。

*值宏引用*可能会出现任何位置 GDL 值中允许规定非文本的空格; 这些引用以等号 （=） 开头。 如果不应引入值宏引用此类的上下文中使用等号，等号必须跟非符号字符 （如空格）。 有关值宏的详细信息，请参阅[GDL 值宏](gdl-value-macros.md)。

有关 GDL 上下文的详细信息，请参阅[GDL 上下文](gdl-contexts.md)。

下面的代码示例显示对 GDL 分析器可接受的值。

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

 

 




