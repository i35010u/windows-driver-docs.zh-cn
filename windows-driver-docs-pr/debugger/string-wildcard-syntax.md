---
title: 字符串通配符语法
description: 本主题介绍了字符串通配符语法。 某些调试器命令具有接受多种通配符字符的字符串参数。
ms.assetid: 11e73f81-5d5c-4d9a-8380-ec767b27f603
keywords: 字符串通配符、 表达式、 正则表达式语法规则的命令
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12885d5b86ac862c940144d2b558c1535f73dedb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335501"
---
# <a name="string-wildcard-syntax"></a>字符串通配符语法


## <span id="ddk_string_wildcard_syntax_dbg"></span><span id="DDK_STRING_WILDCARD_SYNTAX_DBG"></span>


某些调试器命令具有接受多种通配符字符的字符串参数。 其各自的参考页上说明了这些参数。

这些类型的参数支持以下语法功能：

- 一个星号 (\*) 表示零个或多个字符。

- 问号 （？） 表示任何单个字符。

- 方括号 ( \[ \] ) 包含一系列字符表示列表中的任何单个字符。 在列表中的一个字符进行匹配。 在这些方括号内可以使用连字符 （-） 来指定的范围。 例如， **Prog\[er t7\]是**匹配"Progeam"、"程序"、"Progsam"、"Progtam"和"Prog7am"。

- 数字符号 (\#) 表示零个或多个前面的字符。 例如， **Lo\#p**匹配"Lp"、"Lop"、"循环"、"Looop"等。 您也可以组合以数字符号方括号，因此**m\[ia\]\#n**匹配"mn"、"分钟"、"man"、"maan"、"主要"、"mian"、"miin"、"miain"等。

- 加号 （+） 表示一个或多个前面的字符。 例如， **Lo + p**等同于**Lo\#p**，只不过**Lo + p**与"Lp"不匹配。 同样， **m\[ia\]+ n**相同**m\[ia\]\#n**，只不过 m<strong>\[ia\]+ n</strong>与"mn"不匹配。 **？ + b**也是与相同 **\*b**，只不过 **？ + b**与"ab"不匹配。

- 如果你必须指定文本的数字符号 (\#)，问号 （？），打开括号 (\[)，右方括号 (\])，星号 (\*)，或加号 （+） 字符，必须添加一个反斜杠 ( \\ ) 的前面字符。 连字符始终是文本时，不要将它们括在方括号中。 但不能指定文本的连字符用括号括起来的列表中。

指定的符号的参数还支持一些其他功能。 除了标准字符串通配符字符，你可以使用下划线 (\_) 之前使用来指定符号的文本表达式。 在匹配时此表达式与一个符号，调试器将下划线字符视为任意数量的下划线，甚至零。 此功能适用只有当您将匹配的符号。 它不适用于字符串通配符表达式在一般情况下。 有关符号语法的详细信息，请参阅[符号语法和符号匹配](symbol-syntax-and-symbol-matching.md)。

 

 





