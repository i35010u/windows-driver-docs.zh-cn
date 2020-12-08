---
title: GDL 空白字符
description: GDL 空白字符
keywords:
- 构造 WDK GDL，空格字符
- 继续 linebreak WDK GDL
- linebreak 序列 WDK GDL
- 分析器 WDK GDL，处理空白
- GDL WDK，空格字符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 297eee811612033dcb1da0a3434aae345ce747fb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835875"
---
# <a name="gdl-whitespace-characters"></a>GDL 空白字符


*空白字符* 定义为空格、制表符或继续 linebreak。 *继续 linebreak* 是 linebreak 序列，后面紧跟加号 (+) 。  (*linebreak 序列* 为 " \\ n \\ r"、" \\ r \\ n"、" \\ n" 或 " \\ r" 表示为 C 字符串。 ) 

在 [带引号的字符串](gdl-quoted-strings.md) 和任意值上下文中，将按原义解释空白。 出现在其他位置的空白被视为非文本。 GDL 分析器合并非文本空格;也就是说，任意数目的连续非文本空白字符都将替换为一个空格字符。 文本空格不合并。

 

 




