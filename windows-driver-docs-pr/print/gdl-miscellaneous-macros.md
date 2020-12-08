---
title: GDL 其他宏
description: GDL 其他宏
keywords:
- GDL WDK，宏
- 宏 WDK GDL，其他宏
- IgnoreBlock 指令 WDK GDL
- 宏 WDK GDL，示例
- 构造 WDK GDL，禁用构造处理
- 禁用 GDL 构造 WDK GDL 的处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6d5797c428081b6df2e4c40936b0307d6521e4e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835945"
---
# <a name="gdl-miscellaneous-macros"></a>GDL 其他宏


GDL 使用 **\* IgnoreBlock** 指令来禁止处理构造的内容。 当实现除法和治调试策略或注释掉过时的代码时，此指令非常有用。 **\* IgnoreBlock** 的内容仍必须符合基本语法规则。 无效的 GDL 或较大的注释块可以包含在 &lt; Begin/EndValue： &gt; 分隔符内，并将其值设为 **\* IgnoreBlock**。

下面的代码示例演示如何使用 **\* IgnoreBlock**。

```cpp
*IgnoreBlock: <BeginValue:garbage> The code in between does not even need to be valid GDL. }{ " % !!! 
This directive is great for large blocks of comments 
or when you do not want to mark each line with *%  <EndValue:garbage> {}
```

 

 




