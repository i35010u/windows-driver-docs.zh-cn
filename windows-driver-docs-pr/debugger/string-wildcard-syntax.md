---
title: 字符串通配符语法
description: 本主题介绍字符串通配符语法。 某些调试器命令具有接受多种通配符的字符串参数。
keywords: 字符串通配符、表达式、正则表达式、命令语法规则
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d95d0ee44ff39a17d526ed39dbb1a4e7a0413d64
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809677"
---
# <a name="string-wildcard-syntax"></a>字符串通配符语法


## <span id="ddk_string_wildcard_syntax_dbg"></span><span id="DDK_STRING_WILDCARD_SYNTAX_DBG"></span>


某些调试器命令具有接受多种通配符的字符串参数。 这些参数将在各自的参考页上注明。

这些类型的参数支持以下语法功能：

- 星号 (\*) 表示零个或多个字符。

- 问号 (？ ) 表示任何单个字符。

- \[ \] 包含字符列表的方括号 ( ) 表示列表中的任何单个字符。 列表中正好有一个字符匹配。 在这些括号中，可以使用连字符 ( ) 来指定范围。 例如， **\[ 程序 t7 \] Am** 匹配 "Progeam"、"Program"、"Progsam"、"Progtam" 和 "Prog7am"。

- 数字符号 (\#) 表示零个或多个前面的字符。 例如， **Lo \# p** 匹配 "Lp"、"Lop"、"Loop"、"Looop" 等。 还可以将数字符号与方括号组合在一起，以便 **m \[ ia \] \# n** 匹配 "mn"、"min"、"man"、"maan"、"main"、"mian"、"miin"、"miain" 等。

- 加号 (+) 表示一个或多个前面的字符。 例如， **lo + p** 与 **lo \# p** 相同，只不过 **lo + p** 与 "Lp" 不匹配。 同样， **m \[ ia \] + n** 与 **m \[ ia \] \# n** 相同，不同之处在于 m <strong> \[ ia \] + n</strong>与 "mn" 不匹配。 如果？ + **b** 与 "ab" 不匹配，则 **？ + b** 也与 **\* b** 相同。

- 如果需要指定文本数字符号 (\#) 、问号 (？ ) 、左括号 (\[) 、右括号 () \] 、星号 (\*) 或加号 (+) 字符，则必须 \\ 在字符前面添加反斜杠 ( ) 。 当你未将连字符括在括号中时，连字符始终是文本。 但不能在括号内列表中指定文本连字符。

指定符号的参数还支持一些附加功能。 除了标准字符串通配符以外，还可以在 \_ 用来指定符号的文本表达式之前使用下划线 () 。 将此表达式与符号进行匹配时，调试器会将下划线视为任意数量的下划线，甚至是零。 此功能仅适用于匹配符号的情况。 它不会应用于一般的字符串通配符表达式。 有关符号语法的详细信息，请参阅 [符号语法和符号匹配](symbol-syntax-and-symbol-matching.md)。

 

 





