---
title: '#Ifdef 条件预处理器指令'
description: '#Ifdef 条件预处理器指令'
ms.assetid: 57c59bf8-19bd-47bc-858d-ea500d44fb4d
keywords:
- 预处理器指令 WDK GDL，条件指令
- 指令 WDK GDL，条件指令
- 条件指令 WDK GDL
- Ifdef 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c5bc44b021319f0d12036748b2ba9cd25a7a4f7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372913"
---
# <a name="ifdef-conditional-preprocessor-directive"></a>\#Ifdef 条件预处理器指令


```GDL
#Ifdef: symbol
```

\#Ifdef 指令定义的条件构造和部分开始。 如果预处理器符号字典中找到符号，则会保留部分。 如果找不到符号，则将其删除。 *符号*值是必需的。
