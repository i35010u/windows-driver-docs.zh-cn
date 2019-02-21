---
title: '#包括预处理器指令'
description: '#包括预处理器指令'
ms.assetid: 6c3e4de7-2007-4a1a-bdb0-fd5b2b64f489
keywords:
- 预处理器指令 WDK GDL，关键字
- 关键字 WDK GDL
- 保留的关键字 WDK
- Include 指令 WDK GDL
- GDL WDK 源文件
- 源文件 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18d374b689ea256bc5636daffbcc3fc3c0337488
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548188"
---
# <a name="include-preprocessor-directive"></a>\#包括预处理器指令


```GDL
#Include: Quoted String
```

\#Include 指令将导致通过名为 GDL 源文件*带引号的字符串*要加载和处理。 当前 GDL 文件预处理已暂停，直到处理完所包含的文件。 所包含的文件可能会影响通过定义或 undefining 符号预处理主机 GDL 文件的其余部分。

带引号的字符串的语法由 GDL 定义。 带引号的字符串值，不同的值的其他指令，可以扩展到多个行。 *带引号的字符串*是必需的。

\#包括和换行而不是大括号 （}） 必须终止所有指令。

如果您使用 **\*Include**，这是一个旧 GPD 关键字，在主机文件后将预处理包含文件。 如果主机文件需要包含的文件，首先进行预处理，这种处理可能会导致问题。 若要避免此类潜在问题，请始终前缀\#Include 指令与当前的预处理器前缀。

分析器的当前实现允许三种形式的命名文件： 文件的名称，完全限定的路径和部分限定的路径。 如果使用部分限定的路径，路径的起始点建立的当前执行环境。 如果仅使用文件名，将尝试两个起点： 根源文件使用的路径，然后建立的当前执行环境的路径。

请注意，如果预编译的文件包含另一个文件，预编译的文件被视为相对于其包含的文件的根源文件有这样担心。 安装和设置代码可能有附加限制。
