---
title: GDL 块宏
description: GDL 块宏
ms.assetid: c8b8e38d-237f-4c54-a394-148d211237ce
keywords:
- GDL WDK 宏
- 宏 WDK GDL，块宏
- 阻止 WDK GDL 宏
- BlockMacros 指令 WDK GDL
- 宏 WDK GDL，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2e83cae8aa82e517d0e39c17d8a86dd23d55466
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562294"
---
# <a name="gdl-block-macros"></a>GDL 块宏


*阻止宏*用于表示一个或多个 GDL 条目。 中定义\*BlockMacros 构造。

实例名称\*BlockMacros 构造将成为块宏和的大括号中包含的项的名称\*BlockMacros 构造成为所指定块的宏的内容。 宏名称必须是符号名称类型。 必须完成的块宏定义包含的条目。

如果有任何构造的条目，它们必须宏定义中完成。 换而言之，块宏定义的内容不能更改的嵌套级别。

块宏可以包含其他块或值宏定义和除了正常数据条目的命名空间指令。 嵌套的宏定义和命名空间指令会立即开始并不会出现在块宏的内容。

宏块可以包含对其他块或值宏的引用。 实例名称\*BlockMacros 构造可以后接括号括起的形式自变量列表。 对此块宏定义主体内任何形式自变量的任何引用将被符号替换为实际引用块宏时传入的相应参数。

**请注意**  声明和引用将用于将值宏引用传递自变量的前缀为等号 （=） 来表示参数类型是值宏。 对值宏的所有引用以等号，以表示引用的是值宏而不是块宏还作为都前缀。

 

对块宏的引用可以嵌套到任意深度的参数列表。 使用引用块宏\*InsertBlock:NameOfBlockMacro. 使用等号不带前缀块宏的名称，因为它不是对值宏的引用。 此语法不同于 GPD 语法。

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

 

 




