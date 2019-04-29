---
title: 调试器命令程序的元素
description: 调试器命令程序的元素
ms.assetid: f964e358-2f3f-4780-87ea-e1374ae861e6
keywords:
- 调试器命令程序中元素
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 768d0ea10108f11fda5aa334d696ed9d501190be
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323132"
---
# <a name="elements-of-a-debugger-command-program"></a>调试器命令程序的元素


## <span id="ddk_elements_of_a_debugger_command_program_dbg"></span><span id="DDK_ELEMENTS_OF_A_DEBUGGER_COMMAND_PROGRAM_DBG"></span>


一个*调试器命令程序*是包含调试器命令和控制流令牌，例如一个小型应用程序 **.if**， **。 有关**，和 **.while**. (有关控制流令牌及其语法的完整列表，请参阅[控制流令牌](control-flow-tokens.md)。)

你可以使用大括号 ( **{}** ) 括起更大的命令块中的语句块。 当您输入的每个块时，块中的所有别名都评估。 如果稍后更改别名命令块中的值，该点后的命令将不要使用新别名值，除非它们是从属块内。

不能使用一对括号来创建一个块。 您必须添加左大括号前的控制流令牌。 如果你想要创建一个块，只有在要评估的别名，应使用[ **.block** ](-block.md)令牌之前左大括号。

可以使用调试器命令程序[名用户为别名或固定名称的别名](using-aliases.md)作为其本地变量。 如果你想要使用数字或类型化变量，则可以使用 **$t * * * n*[伪寄存器](pseudo-register-syntax.md)。

仅当它们不是其他文本旁边评估用户命名别名。 如果你想要评估其他文本，使用旁边的别名[ **$ {} （别名解释器）** ](-------alias-interpreter-.md)令牌。 此令牌具有可选开关，您可以评估不同的方式中的别名。

可以向调试器命令程序添加注释，通过使用两个美元符号 ([**$$ （注释说明符）**](-----comment-specifier-.md))。 应插入一个令牌和其元素 （如大括号或条件） 之间的注释。

**请注意**  不应使用一个星号 ([  **\* （注释行说明符）**](----comment-line-specifier-.md))。 因为有一个星号指定的注释不以分号结尾，则表示忽略程序的其余部分。

 

通常情况下，应使用调试器命令程序内的 MASM 语法。 当您必须使用C++元素 （例如，指定的结构或类成员），可以使用 **@@c+ + （)** 令牌以切换到C++该子句的语法。

**$Scmp**， **$sicmp**，并 **$spat** MASM 语法中的字符串运算符是特别有用。 有关这些运算符的详细信息，请参阅[MASM 数字和运算符](masm-numbers-and-operators.md)。

 

 





