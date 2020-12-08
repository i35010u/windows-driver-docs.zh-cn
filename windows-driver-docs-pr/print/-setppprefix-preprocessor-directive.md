---
title: '#SetPPPrefix 预处理器指令'
description: '#SetPPPrefix 预处理器指令'
keywords:
- 预处理器指令 WDK GDL，关键字
- 关键字 WDK GDL
- 保留关键字 WDK
- SetPPPrefix 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d34ce7f5b0b85ae1e9418ad9a69e58a9ee7f1115
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806011"
---
# <a name="setppprefix-preprocessor-directive"></a>\#SetPPPrefix 预处理器指令


```GDL
#SetPPPrefix: prefix
```

\#SetPPPrefix 指令将 *前缀* 值作为当前预处理器前缀。 *前缀* 可以是任何标记值，并且是必需的。

可以多次定义同一前缀。 前缀是用户可选的，因为它允许指令明确地有别于任何现有的不处理数据。 下面的代码示例演示如何在正常 GDL 项包含可能与实际指令混淆的值时更改前缀。

```GDL
*%  assume current prefix is #
#SetPPPrefix: #Temp#
#Temp#Ifdef:  WINNT_60
*InfoMessage: "Use the Preprocessor Directive
#PreCompiled to make your GDL file sharable."
#Temp#Endif:  WINNT_60
#Temp#UndefinePrefix
*%  now back to normal # prefix.
```
