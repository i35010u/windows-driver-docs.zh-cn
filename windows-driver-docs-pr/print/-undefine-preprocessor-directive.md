---
title: '#取消定义预处理器指令'
description: '#取消定义预处理器指令'
keywords:
- 预处理器指令 WDK GDL，关键字
- 关键字 WDK GDL
- 保留关键字 WDK
- 取消定义指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14715d6d92cef110302c98f43c385ed3cd3bbd22
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794265"
---
# <a name="undefine-preprocessor-directive"></a>\#取消定义预处理器指令


```GDL
#Undefine: symbol
```

\#取消定义的指令将从预处理器符号字典中删除 *符号* 值。 如果多次定义了符号，则只会删除最新的 *符号* 定义。

*符号* 值是可选的。 如果省略此值，则会删除最近定义的符号。 但是，分隔冒号 (： ) 仍是必需的。
