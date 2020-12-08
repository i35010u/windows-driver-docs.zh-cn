---
title: '#Ifdef 条件预处理器指令'
description: '#Ifdef 条件预处理器指令'
keywords:
- 预处理器指令 WDK GDL，条件指令
- 指令 WDK GDL，条件指令
- 条件指令 WDK GDL
- Ifdef 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e36d9afacc429666a6e8baa35250b4a7e2d2b7a7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794272"
---
# <a name="ifdef-conditional-preprocessor-directive"></a>\#Ifdef 条件预处理器指令


```GDL
#Ifdef: symbol
```

\#Ifdef 指令定义条件构造和节的开头。 如果在预处理器符号字典中找到符号，则保留部分。 如果未找到符号，则将其删除。 *符号* 值是必需的。
