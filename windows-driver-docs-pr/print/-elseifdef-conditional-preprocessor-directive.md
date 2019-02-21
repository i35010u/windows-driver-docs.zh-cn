---
title: '#Elseifdef 条件预处理器指令'
description: '#Elseifdef 条件预处理器指令'
ms.assetid: 0239696a-ea6a-4fd4-b4ca-870a87022c81
keywords:
- 预处理器指令 WDK GDL，条件指令
- 指令 WDK GDL，条件指令
- 条件指令 WDK GDL
- Elseifdef 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f3e30c20e9dc1b300cdc46f0ffd8f94ad152abc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522143"
---
# <a name="elseifdef-conditional-preprocessor-directive"></a>\#Elseifdef 条件预处理器指令


```GDL
#Elseifdef: symbol
```

\#Elseifdef 指令定义了上一节的末尾和新的条件部分开始。 如果预处理器符号字典中找到符号和前一节中构造已被预留，则会保留部分。 如果找不到符号，则构造将被删除。 *符号*值是必需的。
