---
title: '#DisablePPDirective 预处理器指令'
description: '#DisablePPDirective 预处理器指令'
keywords:
- 预处理器指令 WDK GDL，关键字
- 关键字 WDK GDL
- 保留关键字 WDK
- DisablePPDirective 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44dd2c6967f8b7810b635a3ddae287b9b41675d0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812457"
---
# <a name="disableppdirective-preprocessor-directive"></a>\#DisablePPDirective 预处理器指令


```GDL
#DisablePPDirective:    Directive
```

\#DisablePPDirective 指令禁用已启用的指令。 如果新的 GDL 文件包含的 GDL 文件与一个或多个新指令名称的命名空间冲突，则可以在包括文件之前禁用新指令，然后再重新启用。 基名称是必需的值。

此预处理器指令是 GDL 的新指令。

下面的代码示例演示如何使用此指令。

```GDL
#DisablePPDirective: duplicateDirective
#Include: "OlderFile.gdl"  *%  This file uses the name 
    *%  duplicateDirective because it does not expect that name to be interpreted by 
    *%  the preprocessor.
#EnablePPDirective: duplicateDirective
    *%  Reactivate  duplicateDirective  so it can be used by 
    *%  the newer host file.
```

 

 




