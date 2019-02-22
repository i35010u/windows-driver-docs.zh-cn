---
title: GDL 带引号的字符串
description: GDL 带引号的字符串
ms.assetid: 52d6f1bf-0b8c-4aa7-8cc8-1a18def224be
keywords:
- 构造 WDK GDL，字符串
- GDL WDK 字符串
- 字符串 WDK GDL，带引号的字符串
- 带引号的字符串 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0911ff78717c40e1bdc78f39c7fd1a4c2e5306e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555183"
---
# <a name="gdl-quoted-strings"></a>GDL 带引号的字符串


一个*带引号的字符串*开头和结尾的双引号字符 （"）。 有以下例外带引号的字符串的一部分，将按原义视为之间出现的任何字符：

-   百分比符号加上双引号 (%") 将被视为原义双引号字符 （"）。

-   百分比符号和小于号 (%&lt;) 被视为小于符号的文本 (&lt;)。

-   百分比符号后跟任何其他字符被视为文字百分号 （%）。

-   小于符号 (&lt;) 引入了[HexSubString](gdl-hexsubstrings.md)上下文。

-   带引号的字符串可以出现在嵌套的上下文;仅 HexSubString 上下文被识别 uoted 字符串内。

 

 




