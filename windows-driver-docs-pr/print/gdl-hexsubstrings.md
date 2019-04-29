---
title: GDL 十六进制子字符串
description: GDL 十六进制子字符串
ms.assetid: 7451fd1f-a765-486a-bd90-bc01eac2c388
keywords:
- 构造 WDK GDL，字符串
- GDL WDK 字符串
- 字符串 WDK GDL HexSubString
- HexSubString WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 403becf4763b4a4fcd9eb0446c2fd97e44b0146d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372131"
---
# <a name="gdl-hexsubstrings"></a>GDL 十六进制子字符串


一个*HexSubString*是一种方法来表示带引号的字符串中的非可显示字符。 HexSubString 引入的小于号 (&lt;) 并且已被终止的大于号 (&gt;)。

在 HexSubString 上下文中，只有允许的字符是十六进制数字、 空格和 linebreak 序列和延续换行符。 将忽略 HexSubString 上下文中发生的所有空格和 linebreak 字符。 每个 HexSubString 必须包含偶数个十六进制数字，因为两个十六进制数字所需定义一个字节。

如果你想要创建带引号的字符串的末尾百分号 （%），必须使用 HexSubString 表示百分比字符"&lt;25&gt;"。

HexSubString 上下文可以只在带引号的字符串上下文中出现。 注释可以出现在 HexSubString 上下文中。

 

 




