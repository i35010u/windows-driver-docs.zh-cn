---
title: '#Endif 条件预处理器指令'
description: '#Endif 条件预处理器指令'
keywords:
- 预处理器指令 WDK GDL，条件指令
- 指令 WDK GDL，条件指令
- 条件指令 WDK GDL
- Endif 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b39e10fc1bf96e24554211901bd388bf5a882852
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812451"
---
# <a name="endif-conditional-preprocessor-directive"></a>\#Endif 条件预处理器指令


```GDL
#Endif:
```

\#Endif 指令定义上一部分和条件构造的结尾。 不使用任何符号。 您可以使用虚设符号名称作为 \# Endif 指令的值来帮助读者。 请考虑以下代码示例。

```GDL
    #Ifdef: symbolA

        #Ifdef: symbolB

        #Elseifdef: symbolD

        #Endif: symbolB

    #Endif: symbolA
```

每个嵌套构造的缩进也可能对读取器有用。
