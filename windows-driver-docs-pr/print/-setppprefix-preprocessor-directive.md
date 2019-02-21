---
title: '#SetPPPrefix 预处理器指令'
description: '#SetPPPrefix 预处理器指令'
ms.assetid: 3520aa66-1090-40db-9c9f-cfba0e6e2bee
keywords:
- 预处理器指令 WDK GDL，关键字
- 关键字 WDK GDL
- 保留的关键字 WDK
- SetPPPrefix 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c33caffc8f45a09f26373590c2be8c0cf9510409
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547241"
---
# <a name="setppprefix-preprocessor-directive"></a>\#SetPPPrefix 预处理器指令


```GDL
#SetPPPrefix: prefix
```

\#SetPPPrefix 指令使*前缀*值当前预处理器的前缀。 *前缀*可以是任何令牌的值并且是必需的。

可以多次定义相同的前缀。 前缀是用户可选择，因为它允许指令明确区分从处理 not 任何现有数据。 下面的代码示例演示如何更改前缀，如果正常 GDL 条目包含一个值，可能与实际指令相混淆。

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
