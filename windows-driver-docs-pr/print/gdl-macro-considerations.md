---
title: GDL 宏注意事项
description: GDL 宏注意事项
keywords:
- GDL WDK，宏
- 宏 WDK GDL，注意事项
- 传递 GDL 宏引用 WDK
- 宏 WDK GDL，传递宏引用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c84ef0998eb38191a5680c3053a1399c09cfac84
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835951"
---
# <a name="gdl-macro-considerations"></a>GDL 宏注意事项


GDL 宏的作用域和生存期。 只有在包含宏定义构造的嵌套级别结束后，才能从定义点引用宏。

在根级别定义的宏具有无限范围和生存期。 同一命名空间中可以定义具有相同名称的多个宏。 最新的定义将隐藏以前的所有定义。 前面的定义将在最顶层定义过期后被覆盖。

如果块宏定义使用 **\# include 指令来包括预** 编译文件，则该文件的内容将不会出现在宏定义中，因为声明为预编译的文件不会在行中使用，而是成为独立的实体。

为实现向后兼容性，为所有值宏定义启用参数值支持。

宏定义不能引用自身。 但宏引用可以将对自身的引用作为参数传递。

下面的代码示例演示如何传递引用。

```cpp
*InsertBlock:  Myself(Myself(AnotherMacro))
```

 

 




