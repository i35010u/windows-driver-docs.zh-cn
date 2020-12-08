---
title: 语法规则
description: 本部分介绍使用调试器命令时必须遵循的语法规则。
keywords: 命令、语法规则、元命令
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b89ed80202757cdfda3a1ee01e48a5c9774c3adb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833173"
---
# <a name="syntax-rules"></a>语法规则


## <span id="ddk_syntax_rules_dbg"></span><span id="DDK_SYNTAX_RULES_DBG"></span>


本部分介绍使用调试器命令时必须遵循的语法规则。

调试时，应遵循以下常规语法规则：

-   你可以在命令和参数中使用大写字母和小写字母的任意组合，但本部分的主题中特别指出。

-   可以通过一个或多个空格或 **逗号 ()** 来分隔多个命令参数。

-   通常可以忽略命令和其第一个参数之间的空间。 如果省略，则可以经常省略其他空格。

本部分中的命令参考主题使用以下各项：

- **粗体** 字体样式指示必须按原义键入的项。

- *斜体* 字体样式中的字符表示在参考主题的 "parameters" 节中介绍的参数。

- 方括号 () 中的参数 **\[** <em>xxx</em> **\]** 是可选的。 带竖线 (**\[** <em>xxx</em> **|** <em>yyy</em> **\]**) 的方括号指示你可以使用所包含的参数中的一个或无。

- 带有竖线 (**{**<em>xxx</em> **|** <em>yyy</em>**}**) 的大括号，表示必须只使用其中一个括起来的参数。

以下主题描述了以下参数类型使用的语法：

[数字表达式语法](numerical-expression-syntax.md)

[字符串通配符语法](string-wildcard-syntax.md)

[寄存器语法](register-syntax.md)

[伪寄存器语法](pseudo-register-syntax.md)

[源文件行语法](source-line-syntax.md)

[地址和地址范围语法](address-and-address-range-syntax.md)

[线程语法](thread-syntax.md)

[进程语法](process-syntax.md)

[系统语法](system-syntax.md)

[多处理器语法](multiprocessor-syntax.md)

语法还在使用符号方面扮演着重要的角色。 有关更多详细信息，请参阅 [符号语法和符号匹配](symbol-syntax-and-symbol-matching.md)。

 

 





