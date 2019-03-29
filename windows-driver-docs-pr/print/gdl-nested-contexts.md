---
title: GDL 嵌套上下文
description: GDL 嵌套上下文
ms.assetid: c679937a-fa36-487a-84f2-f61a7ef0198e
keywords:
- GDL WDK 上下文
- 上下文 WDK GDL，嵌套的上下文
- 嵌套的上下文 WDL GDL
- GDL WDK 值
- 值 WDK GDL，嵌套的上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f69092e1e218277bce87e0baf2b9c14ec2b39cba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566028"
---
# <a name="gdl-nested-contexts"></a>GDL 嵌套上下文


一个*嵌入的上下文*中引入了*开始嵌套字符*（这是一个左括号或者左方括号）。 嵌入的上下文时结束匹配*结束嵌套字符*遇到 （这是右括号或右方括号）。

嵌套上下文可以相互嵌套。 结束嵌套字符可以是仅用于结束嵌套在当前上下文。 如果结束嵌套字符显示的其他任何位置，它是语法错误。

在嵌套的上下文中，[构造分隔符字符](gdl-construct-delimiters.md)失去其意义构造分隔符以及也被视为嵌入的上下文分隔符。 在嵌套的上下文中，linebreak 序列被视为非文本空格。

之外的任何上下文或另一个嵌套的上下文中但不是能在任何其他上下文中，可以显示嵌套的上下文。 任何上下文，包括其他嵌套的上下文中，可以出现在嵌套的上下文中，除了 HexSubString 上下文。

下面的代码示例显示了 GDL 嵌套的上下文。

```cpp
*good_nests: ( { } [ ( ) ] )
```

下面的代码示例演示 GDL 嵌套包含错误的上下文。

```cpp
*bad_nests: (  ] *%  end nesting delimiter can only be used within its nesting context.
*bad_nests: (  ]  )
*bad_nests:   ] [   *%  end nesting delimiter can only be used within its nesting context.
*bad_nests: (  [  )   ]   *%  end nesting delimiter can only be used within its nesting*% context.  In this case the ')' char cannot be used within the context begun 
*%by '[' .
*bad_nests:  {  [ ]  }  *% attempt to use construct delimiter to define a nesting context 
*%  outside of a nesting context.
```

嵌套的上下文的全部内容视为的一部分[值](gdl-values.md)。 例如，以下 GDL 代码表示使用的关键字的一项"\*KeywordA"。 片段的其余部分是的值\*KeywordA，因为显示为不同的项\*KeywordB 和\*KeywordC 包含嵌套的上下文中。 事实上，数字"12、 38，709"本身就是由外部由左中括号分隔符定义的上下文中嵌套的括号分隔符定义的嵌套上下文中。

```cpp
*KeywordA: [
*KeywordB:  List(12, 38, 709)
*KeywordC:  "the small brown fox" ]
```

 

 




