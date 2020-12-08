---
title: GDL 嵌套上下文
description: GDL 嵌套上下文
keywords:
- GDL WDK，上下文
- 上下文 WDK GDL，嵌套上下文
- 嵌套上下文 WDL GDL
- GDL WDK，值
- 值 WDK GDL，嵌套上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d9eee1d165ce91ce73c2936d4eadde483849688
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835949"
---
# <a name="gdl-nested-contexts"></a>GDL 嵌套上下文


*嵌套上下文* 随 *开始嵌套字符* 一起引入 (这是左括号或左方括号) 。 当匹配的 *结束嵌套字符* (为) 的右括号或右方括号时，嵌套上下文结束。

嵌套上下文可以相互嵌套。 结束嵌套字符只能用来结束当前的嵌套上下文。 如果结束嵌套字符出现在其他位置，则它是一个语法错误。

在嵌套的上下文中， [构造分隔符字符](gdl-construct-delimiters.md) 会失去其含义作为构造分隔符，还会被视为嵌套的上下文分隔符。 在嵌套上下文内，linebreak 序列被视为非文本空白。

嵌套上下文可以出现在任何上下文之外或其他嵌套上下文中，而不能出现在任何其他上下文中。 除 HexSubString 上下文外，任何上下文（包括其他嵌套上下文）都可以出现在嵌套上下文中。

下面的代码示例演示了 GDL 嵌套上下文。

```cpp
*good_nests: ( { } [ ( ) ] )
```

下面的代码示例演示包含错误的 GDL 嵌套上下文。

```cpp
*bad_nests: (  ] *%  end nesting delimiter can only be used within its nesting context.
*bad_nests: (  ]  )
*bad_nests:   ] [   *%  end nesting delimiter can only be used within its nesting context.
*bad_nests: (  [  )   ]   *%  end nesting delimiter can only be used within its nesting*% context.  In this case the ')' char cannot be used within the context begun 
*%by '[' .
*bad_nests:  {  [ ]  }  *% attempt to use construct delimiter to define a nesting context 
*%  outside of a nesting context.
```

嵌套上下文的全部内容被视为 [值](gdl-values.md)的一部分。 例如，下面的 GDL 代码表示一个关键字为 "KeywordA" 的条目 \* 。 片段的其余部分是 KeywordA 的值 \* ，因为 KeywordB 和 KeywordC 的分隔条目应 \* \* 包含在嵌套上下文中。 事实上，数字 "12，38，709" 本身位于嵌套上下文中，后者由嵌套在方括号分隔符定义的外部上下文内的括号分隔符定义。

```cpp
*KeywordA: [
*KeywordB:  List(12, 38, 709)
*KeywordC:  "the small brown fox" ]
```

 

 




