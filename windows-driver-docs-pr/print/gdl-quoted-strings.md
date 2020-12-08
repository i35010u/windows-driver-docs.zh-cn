---
title: GDL 带引号字符串
description: GDL 带引号字符串
keywords:
- 构造 WDK GDL，字符串
- GDL WDK，字符串
- 字符串 WDK GDL，带引号的字符串
- 带引号的字符串 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abb83afa73f5c390030188fc0a631994f788f318
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835937"
---
# <a name="gdl-quoted-strings"></a>GDL 带引号字符串


*带引号的字符串* 以双引号字符开始和结束， ( ") 。 出现在中的任何字符将按原义形式视为引号字符串的一部分，但以下情况例外：

-   百分号和双引号 (% ") 被视为文本双引号 (" ) 。

-   百分比符号加上小于符号 (% &lt;) 被视为小于符号 (&lt;) 。

-   后跟任何其他字符的百分号符号被视为文本百分比符号 (% ) 。

-   小于符号 (&lt;) 引入 [HexSubString](gdl-hexsubstrings.md) 上下文。

-   带引号的字符串可以出现在嵌套的上下文中;在 uoted 字符串内只能识别 HexSubString 上下文。

 

 




