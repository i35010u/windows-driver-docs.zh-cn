---
title: '#Elseifdef 条件预处理器指令'
description: '#Elseifdef 条件预处理器指令'
keywords:
- 预处理器指令 WDK GDL，条件指令
- 指令 WDK GDL，条件指令
- 条件指令 WDK GDL
- Elseifdef 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 163b7cc5eb824b7d64160b99b4446240843b60fb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812453"
---
# <a name="elseifdef-conditional-preprocessor-directive"></a>\#Elseifdef 条件预处理器指令


```GDL
#Elseifdef: symbol
```

\#Elseifdef 指令定义上一节的末尾和新条件节的开头。 如果在预处理器符号字典中找到该符号并且未保留构造中的上一部分，则会保留该部分。 如果未找到符号，则将删除该构造。 *符号* 值是必需的。
