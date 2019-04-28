---
title: GDL 其他宏
description: GDL 其他宏
ms.assetid: d3c66bc1-815d-484b-b69b-6616d2b43069
keywords:
- GDL WDK 宏
- 宏 WDK GDL，杂项宏
- IgnoreBlock 指令 WDK GDL
- 宏 WDK GDL，示例
- 构造 WDK GDL，禁用的构造处理
- 禁用 GDL 处理构造 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 307e3ef168ca7f47488edbc273ceb1c93fa11525
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338360"
---
# <a name="gdl-miscellaneous-macros"></a>GDL 其他宏


使用 GDL  **\*IgnoreBlock**指令以禁用构造的内容的处理。 当实现分而治之调试策略时，此指令很有用或注释掉已过时的代码。 内容 **\*IgnoreBlock**仍必须遵守的基本语法规则。 无效 GDL 或大型的注释块可以括起&lt;Begin/EndValue:&gt;分隔符的值进行 **\*IgnoreBlock**。

下面的代码示例演示如何使用 **\*IgnoreBlock**。

```cpp
*IgnoreBlock: <BeginValue:garbage> The code in between does not even need to be valid GDL. }{ " % !!! 
This directive is great for large blocks of comments 
or when you do not want to mark each line with *%  <EndValue:garbage> {}
```

 

 




