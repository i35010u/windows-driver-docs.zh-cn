---
title: '#包含预处理器指令'
description: '#包含预处理器指令'
keywords:
- 预处理器指令 WDK GDL，关键字
- 关键字 WDK GDL
- 保留关键字 WDK
- Include 指令 WDK GDL
- GDL WDK，源文件
- 源文件 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9be56fab65e28fac9b1a05128a82afdbf558055
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812449"
---
# <a name="include-preprocessor-directive"></a>\#包含预处理器指令


```GDL
#Include: Quoted String
```

\#Include 指令导致加载和处理用 *引用的字符串* 命名的 GDL 源文件。 当前 GDL 文件的预处理暂停，直到处理完包含的文件。 包含的文件可通过定义或 undefining 符号，影响主机 GDL 文件的其余部分的预处理。

带引号的字符串的语法由 GDL 定义。 与其他指令的值不同，带引号的字符串值可以跨多行扩展。 需要 *带引号的字符串*。

\#Include 和 all 指令必须以换行符结尾，而不是用大括号 (} ) 。

如果使用 **\* include**，这是一个旧的 GPD 关键字，则会在主机文件后对包含文件进行预处理。 如果主机文件要求首先预处理包含的文件，此处理可能会导致问题。 若要避免此类潜在问题，请始终在 \# Include 指令前面添加当前预处理器前缀。

分析器的当前实现允许三种形式的文件命名：仅文件名、完全限定路径和部分限定路径。 如果使用部分限定的路径，则该路径的起始点由当前执行环境建立。 如果仅使用文件名，则将尝试两个起始点：根源文件使用的路径，以及当前执行环境所建立的路径。

请注意，如果预编译文件包含其他文件，则会将预编译文件视为相对于其所包含文件的根源文件。 安装代码和安装代码可能会施加其他限制。
