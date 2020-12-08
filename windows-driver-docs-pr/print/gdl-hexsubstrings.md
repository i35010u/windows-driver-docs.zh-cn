---
title: GDL 十六进制子字符串
description: GDL 十六进制子字符串
keywords:
- 构造 WDK GDL，字符串
- GDL WDK，字符串
- 字符串 WDK GDL，HexSubString
- HexSubString WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85571aa091766607bb81c6de25d7850a866a1ca8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796993"
---
# <a name="gdl-hexsubstrings"></a>GDL 十六进制子字符串


*HexSubString* 是一种表示带引号的字符串中不可显示字符的方法。 HexSubString 是由小于符号 () 引入的 &lt; ，由大于符号 (&gt;) 终止。

在 HexSubString 上下文中，允许的唯一字符是十六进制数字、空格和 linebreak 序列以及延续换行符。 在 HexSubString 上下文中出现的所有空白字符和 linebreak 字符都将被忽略。 每个 HexSubString 都必须包含偶数个十六进制数字，因为定义单个字节需要两个十六进制数字。

若要创建以百分号 (% ) 结尾的带引号的字符串，则必须用 HexSubString "25" 表示百分比字符 &lt; &gt; 。

HexSubString 上下文只能出现在带引号的字符串上下文中。 注释可以出现在 HexSubString 的上下文中。

 

 




