---
title: GDL 宏参数
description: GDL 宏参数
ms.assetid: 2aeaf2fd-39e3-4661-85d1-ccb855a73044
keywords:
- GDL WDK 宏
- WDK GDL，自变量的宏
- 宏 WDK GDL，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3873dcdfe75311ca533f452f4a3ac180777fc664
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526041"
---
# <a name="gdl-macro-arguments"></a>GDL 宏参数


宏定义的内容可以引用所有，一些，或者没有任何其形式自变量，尤其是对于值宏定义，可能发生多个值宏定义中一个\*宏构造与单个的形式自变量列表由定义的所有共享。 在这种情况下，一个定义可以引用一些形式自变量，同时另一个引用 none。

如果宏定义中省略对一个或多个形式自变量的引用，该宏引用时提供的参数列表可以由逗号 （，） 分隔执行任何操作的指示这些缺少的参数。

例如，以下宏引用使用仅第五个参数。 前四个被省略。

```cpp
*Attribute: =Macro(,,,, =PassedInMacroRef)
```

不需要在所有表示尾随省略的参数。 如果上一示例中的宏声明 10 个形式自变量，但引用仅第五个参数，前面的示例中将仍将引用该宏的有效方式。

对于值宏，宏引用和其参数列表之间允许不含空格。 此语法，分析器来区分的宏引用使用任何参数，碰巧跟内容如下所示的参数列表中，使用的参数列表的宏引用。

例如，考虑下面的代码示例。

```cpp
*Attrib:   =Macro1 (=Macro2)       *%  is 2 separate macro references
    while
*Attrib:   =Macro1(=Macro2)        *% you are passing Macro2 as a 
    *%  parameter  to Macro1.
```

如果嵌套的宏定义，形式自变量可以使用仅由声明自变量的宏的内容。 嵌套的宏定义中的内容不能引用封闭宏定义的参数。

在宏定义中出现的宏引用可以包含命名宏本身需要参数列表的参数列表。 但是，不能为对形式自变量的引用提供的参数列表。 例如，块宏定义中的以下项是可接受的。

```cpp
*Attrib1: =Macro1(=Macro2(=Macro3(=Arg1, =Arg2)))
```

在前面的示例中，= 长音符表示对先前定义的值宏的引用和 = ArgN 表示对的形式自变量的引用。

但是，下面的代码示例不是一个可接受的条目。

```cpp
*Attrib2: =Arg1(=Arg2, =Arg3(=Macro1, =Macro2))   *%  Not Valid !
```

如果宏引用与该宏声明的正式参数名称相匹配，您可以假定它是对该形式自变量，而不考虑实际宏是否存在具有该名称的引用。 可以通过使用与宏引用命名空间限定符来避免这种多义性。 但是，不能使用形式自变量命名空间限定符。

对于值宏，如果没有形式自变量列表中已声明\*宏构造，任何对中定义的宏的引用不应遵循与参数列表。 此列表将不被视为宏引用的一部分。

例如，如果认为 = Macro1 由下面的代码示例。

```cpp
*Macros:   NoArgList
{
Macro1:  "a Value macro with no argument list"
Macro2:  "a Value macro with no argument list"
Macro3:  "a Value macro with no argument list"
}
```

然后，以下宏引用将被解释为三个单独的和不相关的宏引用。

```cpp
*attribute:  =Macro1(=Macro2, =Macro3)
```

分析器不进行解释 （= Macro2，= Macro3） 是参数列表 = Macro1。 此行为将保留当前 GPDs 向后的兼容。

 

 




