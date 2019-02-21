---
title: GDL 宏注意事项
description: GDL 宏注意事项
ms.assetid: b1e3e32f-2f5f-47ae-b69b-7645ada59c2a
keywords:
- GDL WDK 宏
- 宏 WDK GDL，注意事项
- 传递 GDL 宏引用 WDK
- 宏 WDK GDL，传递宏引用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a249c243574095846b55ee3f0e9022f27a9aa6e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533713"
---
# <a name="gdl-macro-considerations"></a>GDL 宏注意事项


GDL 宏所具有的作用域和生存期。 只能从定义中包含宏的定义构造的嵌套级别结束的点，可以引用宏。

宏在根级别定义的具有不受限制的范围和生存期。 可以在同一个命名空间中定义具有相同名称的多个宏。 较新的定义隐藏任何前面的定义。 最顶层定义过期后，前面的定义将为未覆盖。

如果使用的块宏定义**\#包括**指令以包括预编译的文件，该文件的内容不会出现在宏定义中因为使用行中未声明为预编译为的文件但会成为独立的实体。

为了向后兼容，参数值支持功能的所有值宏定义。

宏定义不能引用自身。 但是，宏引用可以作为参数传递到其自身的引用。

下面的代码示例演示如何传递的引用。

```cpp
*InsertBlock:  Myself(Myself(AnotherMacro))
```

 

 




