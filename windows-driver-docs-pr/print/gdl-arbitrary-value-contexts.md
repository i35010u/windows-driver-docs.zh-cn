---
title: GDL 任意值上下文
description: GDL 任意值上下文
ms.assetid: 6de79b2b-5f0f-4d6c-8a95-d9ef2266c2ef
keywords:
- GDL WDK 上下文
- WDK GDL，任意值上下文的上下文
- 任意值上下文 WDK GDL
- WDK GDL，上下文的值
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87476d59772c779e52899e3a05f6a678c68234e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543971"
---
# <a name="gdl-arbitrary-value-contexts"></a>GDL 任意值上下文


*任意值上下文*用于定义包含任何任意字符序列，即使他们违反 GDL 语法规则的值。

引入了任意值上下文时"&lt;BeginValue:*符号*&gt;"字符序列遇到和时终止"&lt;EndValue:*符号*&gt;"遇到字符序列。 *符号*是你选择的任何有效符号令牌。 相同的符号必须出现在 BeginValue 和 EndValue 调用。 无空格可以出现在 BeginValue 和 EndValue 标记。

可以在除注释或带引号的字符串中的任何值上下文中定义的任意值上下文。 任意值上下文可以出现在嵌套的上下文中。 没有上下文识别在任意值，但在中定义任何字节的序列。

任意值上下文符号是一个令牌，从集中的字符组成\[A-Z、 a-z、 0-9 \_ \]。 符号的长度没有限制。

 

 




