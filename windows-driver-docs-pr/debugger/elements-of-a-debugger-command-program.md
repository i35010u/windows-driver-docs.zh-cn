---
title: 调试器命令程序的元素
description: 调试器命令程序的元素
keywords:
- 调试器命令程序，元素
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 413d058436a6d3eff1aa5970f74fa9cd407976da
ms.sourcegitcommit: 83a11e69f7b175011d032a179e4cfa6d5ede9ac2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/01/2021
ms.locfileid: "106113645"
---
# <a name="elements-of-a-debugger-command-program"></a>调试器命令程序的元素

*调试器命令程序* 是一个小型应用程序，其中包含调试器命令和控制流标记，如 **。如果** 为，则为; 如果 **为**，则 **为。**  (有关控制流令牌及其语法的完整列表，请参阅 [控制流令牌](control-flow-tokens.md)。 ) 

你可以使用大括号 ( **{}** ) 将语句块置于更大的命令块中。 输入每个块后，将对块内的所有别名进行评估。 如果以后在命令块中更改别名的值，则在该点之后的命令将不使用新的别名值，除非它们位于从属块内。

不能使用一对大括号创建块。 必须在左大括号前添加一个控制流标记。 如果只想创建一个块来计算别名，则应在左大括号前使用 [**. 块**](-block.md) 标记。

调试器命令程序可以使用 [用户命名的别名或固定名称的别名](using-aliases.md) 作为本地变量。 如果要使用数值或类型化变量，可以使用 **$t**_n_[伪寄存器](pseudo-register-syntax.md)。

仅当不在其他文本旁边时才会计算用户命名的别名。 如果要评估其他文本旁边的别名，请使用 [**$ {} (别名解释器)**](-------alias-interpreter-.md) 令牌。 此令牌包含可选的开关，使你能够以多种方式评估别名。

您可以使用两个货币符号 ([**$ $ (注释说明符)**](-----comment-specifier-.md)) 向调试器命令程序添加注释。 不应在标记及其元素之间插入注释 (例如大括号或条件) 。

**注意**  不应使用星号 () ) [**\* (注释行说明符**](----comment-line-specifier-.md)。 由于用星号指定的注释不以分号结尾，因此将忽略该程序的其余部分。

通常，应在调试器命令程序中使用 MASM 语法。 如果必须使用 c + + 元素 (例如指定结构或类) 的成员，则可以使用 **@ @c + + ( )** 标记来切换到该子句的 c + + 语法。

MASM 语法中的 **$scmp**、 **$sicmp** 和 **$spat** 字符串运算符特别有用。 有关这些运算符的详细信息，请参阅 [MASM 数字和运算符](masm-numbers-and-operators.md)。

 

 





