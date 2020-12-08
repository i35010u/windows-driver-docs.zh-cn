---
title: 访问局部变量
description: 访问局部变量
keywords:
- 局部变量，访问
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3e3ed23e4c0ff8805e96d2a7932543c207b2253
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824371"
---
# <a name="accessing-local-variables"></a>访问局部变量


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


局部变量（如全局变量）存储在符号文件中。 与全局变量一样，调试器会将其名称解释为地址。 可以采用与全局变量相同的方式读取和写入它们。 但是，如果您需要向命令指示某个符号为本地符号，则在符号前面加上一个美元符号 ( $ ) 并 ( 惊叹号！ ) ，如中所示 `$!var` 。

Visual Studio 和 WinDbg 提供了用户界面元素，你可以使用这些元素 (除了) 的命令之外，还可以查看和编辑局部变量。 有关详细信息，请参阅 [查看和编辑内存和在 Visual Studio 中注册](viewing-memory--variables--and-registers-in-visual-studio.md) 和在 [WinDbg 中查看和编辑局部变量](locals-window.md)。

你还可以使用以下方法来显示、更改和使用局部变量：

-   [**Dv (显示局部变量)**](dv--display-local-variables-.md)命令显示所有局部变量的名称和值。

-   [**对于 \_ 每个 \_ 本地**](-for-each-local.md)扩展，可以重复执行单个命令，每个局部变量一次。

但是，局部变量和全局变量之间存在一个主要区别。 当应用程序正在执行时，本地变量的意义取决于程序计数器的位置，因为此类变量的作用域只扩展到定义这些变量的函数。

调试器根据 [本地上下文](changing-contexts.md#local-context)解释局部变量。 默认情况下，此上下文与程序计数器的位置相匹配。 但调试器可以更改上下文。 有关本地上下文的详细信息，请参阅本地上下文。

当更改本地上下文时，将立即更新 "局部变量" 窗口以反映新的本地变量集合。 [**Dv**](dv--display-local-variables-.md)命令还显示新变量。 然后，先前介绍的内存命令会正确解释所有这些变量名称。 然后，可以对这些变量进行读取或写入。

 

 





