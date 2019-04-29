---
title: '#预编译的预处理器指令'
description: '#预编译的预处理器指令'
ms.assetid: 639db56d-7677-4d21-8329-a0f35d68151e
keywords:
- 预处理器指令 WDK GDL，关键字
- 关键字 WDK GDL
- 保留的关键字 WDK
- 预编译的指令 WDK GDL
- GDL WDK 源文件
- 源文件 WDK GDL
- 预编译源文件 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34ab932722f694e8d59dfcb5d6fba449fcd8afaf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372905"
---
# <a name="precompiled-preprocessor-directive"></a>\#预编译的预处理器指令


```GDL
#PreCompiled:  BOOL
```

\#预编译指令指定是否编译源文件。

如果*BOOL*是**TRUE**，假定源代码文件以进行预编译。 否则为如果通过引用源文件[ \#Include](-include-preprocessor-directive.md)指令，该文件是包含在行中。

\#预编译指令必须出现在任何之前[ \#Include](-include-preprocessor-directive.md)指令 GDL 源代码文件中; 否则为它将被忽略。 *BOOL*值是必需的。

文件标记为预编译将根上下文中进行分析。 也就是说，由主机或 GDL 文件包括建立任何上下文都将丢失。 例如，如果主机 GDL 文件包含预编译的文件之前先定义预处理器符号，这些符号不会存在时预编译的文件进行分析。 此类型的解析可确保不能通过使用创建多个预编译的文件版本[ \#Ifdef](-ifdef-conditional-preprocessor-directive.md)块和具有不同的主机定义不同的符号，用于访问各种\#Ifdef 块. 因为预编译的文件永远不会被重新分析，将只有一个唯一的版本。 因此，预编译的文件的编写器必须依赖于任何外部定义的预处理器符号。

此外请注意，预编译文件必须是唯一，并且它们必须是独立于主机包含它们。 预编译的文件不要依赖主机文件引用任何包含的内容或可能在主机文件中定义的任何内容。

此预处理器指令是 GDL 的新增功能。
