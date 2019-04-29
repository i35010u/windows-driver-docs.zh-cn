---
title: '#取消定义预处理器指令'
description: '#取消定义预处理器指令'
ms.assetid: 78f6a895-2c30-4a6f-8916-4c18e22e4e70
keywords:
- 预处理器指令 WDK GDL，关键字
- 关键字 WDK GDL
- 保留的关键字 WDK
- 取消指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 182639dbe6432a355349c51b5a24eb8782dfd4a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372917"
---
# <a name="undefine-preprocessor-directive"></a>\#取消定义预处理器指令


```GDL
#Undefine: symbol
```

\#取消定义指令移除*符号*预处理器符号字典中的值。 如果定义了符号多次，只有最新的定义*符号*中删除。

*符号*值是可选的。 如果省略此值时，会删除最新定义的符号。 但是，分隔冒号 （:）仍需要。
