---
title: GDL 块宏
description: GDL 块宏
keywords:
- GDL WDK，宏
- 宏 WDK GDL，阻止宏
- 阻止宏 WDK GDL
- BlockMacros 指令 WDK GDL
- 宏 WDK GDL，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c017aad55b97358ec0c6415a6ea27c1c38a5cdc3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797042"
---
# <a name="gdl-block-macros"></a>GDL 块宏


*块宏* 用于表示一个或多个 GDL 条目。 它们是在 BlockMacros 构造中定义的 \* 。

BlockMacros 构造的实例名称 \* 成为 block 宏的名称，BlockMacros 构造的大括号中包含的项将 \* 成为该块宏的内容。 宏名必须是符号名称类型。 包含在块宏定义中的项必须是完整的。

如果有任何构造项，则它们必须在宏定义中完成。 换言之，block 宏定义的内容无法更改嵌套级别。

块宏除了包含普通数据条目外，还可以包含其他块或值宏定义和命名空间指令。 嵌套的宏定义和命名空间指令会立即进行计算，且不会出现在 block 宏的内容中。

块宏可以包含对其他块或值宏的引用。 BlockMacros 构造的实例名称 \* 后面可以跟一个用括号括起来的形参列表。 在实际引用块宏时传入的相应参数将符号替换对此块宏定义正文中任何形参的引用。

**注意**  将用于传递值宏引用的参数的声明和引用以等号 (=) 为前缀，表示参数类型为值宏。 对值宏的所有引用也以等号为前缀，以表示引用是值宏而不是块宏。

 

对块宏的引用可以将参数列表嵌套到任意深度。 使用 \* InsertBlock： NameOfBlockMacro 引用块宏。 块宏的名称不带有等号前缀，因为它不是对值宏的引用。 此语法不同于 GPD 语法。

下面的代码示例演示如何使用块宏。

```cpp
*Macros:
{
  LetterName: Letter
  Quote: <BeginValue:Q>"<EndValue:Q>
}
*BlockMacro: LetterSize
{
*Name: =Quote=LetterName=Quote
  *PaperDimension:  PAIR(8.5 , 11)
}
*BlockMacro: PaperOption(PaperSize, =PaperName)
{
  *Option: =PaperName
  {
    *InsertBlock: PaperSize
  }
}

*InsertBlock: PaperOption(LetterSize, =LetterName)
```

 

 




