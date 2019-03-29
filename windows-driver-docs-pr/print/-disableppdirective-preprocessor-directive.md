---
title: '#DisablePPDirective 预处理器指令'
description: '#DisablePPDirective 预处理器指令'
ms.assetid: 5f85a6b1-a72f-45e2-901a-7bce94b4793c
keywords:
- 预处理器指令 WDK GDL，关键字
- 关键字 WDK GDL
- 保留的关键字 WDK
- DisablePPDirective 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a549073bed18cc5981ca1e931c9409a85ffe3366
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575960"
---
# <a name="disableppdirective-preprocessor-directive"></a>\#DisablePPDirective 预处理器指令


```GDL
#DisablePPDirective:    Directive
```

\#DisablePPDirective 指令禁用已启用的指令。 如果新 GDL 文件包含具有与一个或多个新指令名称的命名空间冲突的较旧 GDL 文件，可以禁用包含该文件之前和之后再重新启用新指令。 基名称是必需的值。

此预处理器指令是 GDL 的新增功能。

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

 

 




