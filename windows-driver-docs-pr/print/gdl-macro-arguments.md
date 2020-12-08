---
title: GDL 宏参数
description: GDL 宏参数
keywords:
- GDL WDK，宏
- 宏 WDK GDL，参数
- 宏 WDK GDL，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 160b2702adde549890ff79d392bc4872594f6113
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796991"
---
# <a name="gdl-macro-arguments"></a>GDL 宏参数


宏定义的内容可以引用全部、部分或不引用其任何形参，特别是对于值宏定义，其中，多个值宏定义可以出现在一个宏构造中，其中的 \* 单个形参列表由所有定义共享。 在这种情况下，一个定义可以引用某些形参，而另一个定义不引用。

如果宏定义省略了对一个或多个形参的引用，则在引用宏时提供的参数列表可以通过逗号指示这些缺少的参数 (，) 不区分任何内容。

例如，下面的宏引用仅使用第五个参数。 省略前四个。

```cpp
*Attribute: =Macro(,,,, =PassedInMacroRef)
```

根本不需要指示尾随的省略参数。 如果上一个示例中的宏声明了10个形参但仅引用第五个参数，则前面的示例仍是引用宏的有效方法。

对于值宏，宏引用和其参数列表之间不允许有空格。 此语法使分析器能够区分不使用任何自变量的宏引用，该引用后面跟有使用参数列表的宏引用的参数列表。

例如，请看下面的代码示例。

```cpp
*Attrib:   =Macro1 (=Macro2)       *%  is 2 separate macro references
    while
*Attrib:   =Macro1(=Macro2)        *% you are passing Macro2 as a 
    *%  parameter  to Macro1.
```

如果宏定义是嵌套的，则形参只能由声明参数的宏的内容使用。 嵌套宏定义的内容不能引用封闭宏定义所定义的参数。

宏定义内发生的宏引用可以包含命名宏的参数列表，这些参数列表本身需要参数列表。 但是，不能为引用形参列表提供形参列表。 例如，block 宏定义中的以下条目是可接受的。

```cpp
*Attrib1: =Macro1(=Macro2(=Macro3(=Arg1, =Arg2)))
```

在前面的示例中，= 长长表示对先前定义的值宏的引用，= ArgN 表示对形参的引用。

但是，下面的代码示例并不是可接受的条目。

```cpp
*Attrib2: =Arg1(=Arg2, =Arg3(=Macro1, =Macro2))   *%  Not Valid !
```

如果宏引用与宏声明的形参名称匹配，则可以假定它是对该形参的引用，而不考虑是否存在具有该名称的实际宏。 可以通过将命名空间限定符与宏引用结合使用来避免此类歧义。 但是，不能将命名空间限定符用于形参。

对于值宏，如果未在宏构造中声明任何形参表 \* ，则在中定义的宏的任何引用都不应跟在参数列表的后面。 此类列表将不被视为宏引用的一部分。

例如，考虑以下代码示例是否定义了 = Macro1。

```cpp
*Macros:   NoArgList
{
Macro1:  "a Value macro with no argument list"
Macro2:  "a Value macro with no argument list"
Macro3:  "a Value macro with no argument list"
}
```

然后，将下面的宏引用解释为三个单独且不相关的宏引用。

```cpp
*attribute:  =Macro1(=Macro2, =Macro3)
```

分析器不会将 (= Macro2，= Macro3) 解释为 = Macro1 的参数列表。 此行为可保持与当前 GPDs 的向后兼容性。

 

 




