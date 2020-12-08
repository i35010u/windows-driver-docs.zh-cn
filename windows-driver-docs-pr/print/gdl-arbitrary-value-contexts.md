---
title: GDL 任意值上下文
description: GDL 任意值上下文
keywords:
- GDL WDK，上下文
- 上下文 WDK GDL，任意值上下文
- 任意值上下文 WDK GDL
- 值 WDK GDL，上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a0e546391e542909663ab52b3d4c1174d18a911
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797051"
---
# <a name="gdl-arbitrary-value-contexts"></a>GDL 任意值上下文


*任意值上下文* 用于定义包含任意任意字符序列的值，即使它们违反 GDL 语法规则也是如此。

当 &lt; 遇到 "BeginValue：*symbol*" 字符序列时，将引入任意值上下文 &gt; ，并在 &lt; 遇到 "EndValue：*symbol* &gt; " 字符序列时终止。 *符号* 是所选择的任何有效符号标记。 BeginValue 和 EndValue 调用中必须同时出现相同的符号。 BeginValue 和 EndValue 标记中不能出现空格。

任意值上下文都可以在任何值上下文中定义，注释或带引号的字符串中除外。 任意值上下文可以出现在嵌套的上下文中。 在任意值上下文中都不能识别上下文，但任何字节序列都可以在内定义。

任意值上下文符号是一个标记，它包含集 a-z \[ ，a-z，0-9，中的字符 \_ \] 。 符号长度没有限制。

 

 




