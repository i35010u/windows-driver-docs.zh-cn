---
title: GDL 空白字符
description: GDL 空白字符
ms.assetid: 703c41c0-3e12-465a-823f-c32990a52382
keywords:
- 构造 WDK GDL，空白字符
- 延续 linebreak WDK GDL
- linebreak 序列 WDK GDL
- 分析器 WDK GDL，处理空白
- GDL WDK，空白字符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 652c91e476f1d749ceb567b20ecfdfafc200b64a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566213"
---
# <a name="gdl-whitespace-characters"></a>GDL 空白字符


*空白字符*定义为在空格、 制表符或延续 linebreak。 一个*延续 linebreak*是加号 （+） 后面紧跟 linebreak 序列。 (A *linebreak 序列*是"\\n\\r"、"\\r\\n"，"\\n"，或"\\r"表示为 C 字符串。)

在按原义解释空格[带引号的字符串](gdl-quoted-strings.md)和任意值上下文中。 出现在其他位置的空格被视为非文本。 GDL 分析器将合并非文本空格;也就是说，任意数量的连续非文本空白字符将替换为一个空格字符。 不合并文本的空白。

 

 




