---
title: '#预编译的预处理器指令'
description: '#预编译的预处理器指令'
keywords:
- 预处理器指令 WDK GDL，关键字
- 关键字 WDK GDL
- 保留关键字 WDK
- 预编译的指令 WDK GDL
- GDL WDK，源文件
- 源文件 WDK GDL
- 预编译的源文件 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8664e0f4a405c7a03cb852a1cdd4bab14f0bc077
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812439"
---
# <a name="precompiled-preprocessor-directive"></a>\#预编译的预处理器指令


```GDL
#PreCompiled:  BOOL
```

\#预编译指令指定是否预编译源文件。

如果 *布尔* 值为 **TRUE**，则假定源文件为预编译。 否则，如果通过[ \# Include](-include-preprocessor-directive.md)指令引用源文件，则文件将包含在行中。

\#预编译指令必须出现在 GDL 源文件中的任何[ \# Include](-include-preprocessor-directive.md)指令之前; 否则将被忽略。 *布尔* 值是必需的。

标记为预编译的文件将在根上下文中进行分析。 也就是说，主机或包含 GDL 文件所建立的任何上下文都将丢失。 例如，如果主机 GDL 文件在包含预编译文件之前定义预处理器符号，则在分析预编译文件时，这些符号将不存在。 这种类型的解析可确保不能使用[ \# Ifdef](-ifdef-conditional-preprocessor-directive.md)块创建预编译文件的多个版本，并且具有不同的主机定义不同的符号来访问各种 \# Ifdef 块。 由于预编译文件从不被重新分析，因此将只有一个唯一版本。 因此，预编译文件的编写器不能依赖于任何外部定义的预处理器符号。

另请注意，预编译文件必须唯一，并且它们必须独立于包含它们的主机。 预编译文件不依赖于主机文件引用的任何包含内容，也不依赖于主机文件中可能定义的任何内容。

此预处理器指令是 GDL 的新指令。
