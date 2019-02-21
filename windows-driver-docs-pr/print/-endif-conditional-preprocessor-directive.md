---
title: '#Endif 条件预处理器指令'
description: '#Endif 条件预处理器指令'
ms.assetid: dfbfdb4a-955b-4ccf-b496-c8c5ddc42d2b
keywords:
- 预处理器指令 WDK GDL，条件指令
- 指令 WDK GDL，条件指令
- 条件指令 WDK GDL
- Endif 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e0cdd94f53537150477bfb32ba482c1df14ad1f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546475"
---
# <a name="endif-conditional-preprocessor-directive"></a>\#Endif 条件预处理器指令


```GDL
#Endif:
```

\#Endif 指令定义的上一节和条件构造结束。 使用无符号。 可以为的值使用虚设的符号名称\#Endif 指令来帮助读者。 请考虑下面的代码示例。

```GDL
    #Ifdef: symbolA

        #Ifdef: symbolB

        #Elseifdef: symbolD

        #Endif: symbolB

    #Endif: symbolA
```

每个嵌套构造的缩进也可能对读取器有帮助。
