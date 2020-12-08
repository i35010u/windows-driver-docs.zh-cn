---
title: 按虚拟地址访问内存
description: 按虚拟地址访问内存
keywords:
- 虚拟地址，访问内存
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72758541abb41588adddd683e70450d30721c0c8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824365"
---
# <a name="accessing-memory-by-virtual-address"></a>按虚拟地址访问内存


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


若要访问内存地址或地址范围，可以使用多个命令。 Visual Studio 和 WinDbg 提供 (的用户界面元素以及可用于查看和编辑内存的命令) 。 有关详细信息，请参阅 [查看和编辑内存和在 Visual Studio 中注册](viewing-memory--variables--and-registers-in-visual-studio.md) 和在 [WinDbg 中查看和编辑内存](memory-window.md)。

以下命令可以读取或写入各种格式的内存。 这些格式包括十六进制字节、单词 (单词、双字和四字) 、整数 (短、长、四个整数和无符号整数) 、浮点数 (10 字节、16字节、32-字节和64字节的实数) 和 ASCII 字符。

-   [**D \* (显示内存)**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令显示指定内存地址或范围的内容。

-   [**E \* (输入值)**](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md)命令将值写入指定的内存地址。

您可以使用以下命令来处理更专业化的数据类型：

-   [**Dt (显示类型)**](dt--display-type-.md)命令查找各种数据类型，并显示由正在调试的应用程序创建的数据结构。 此命令的用途非常广泛，并且具有许多变体和选项。

-   [**Ds、ds (显示字符串)**](ds--ds--display-string-.md)命令显示字符串、ANSI \_ 字符串或 UNICODE \_ 字符串数据结构。

-   [**Dl (显示)**](dl--display-linked-list-.md)命令跟踪的链接列表，并显示链接列表。

-   [**D \* s (显示单词和符号)**](dds--dps--dqs--display-words-and-symbols-.md)命令查找可能包含符号信息的双引号或四字，然后显示数据和符号信息。

-   [**！ Address**](-address.md) extension 命令显示有关位于特定地址的内存属性的信息。

您可以使用以下命令来操纵内存范围：

-   [**M (移动内存)**](m--move-memory-.md)命令将一个内存范围的内容移动到另一个内存范围。

-   [**F (Fill memory)**](f--fp--fill-memory-.md)命令向内存范围写入模式，重复此模式直到范围已满。

-   [**C (比较内存)**](c--compare-memory-.md)命令比较两个内存范围的内容。

-   [**(Search Memory)**](s--search-memory-.md)命令在内存范围内搜索指定模式，或搜索内存范围中存在的任何 ASCII 或 Unicode 字符。

-   [**Holdmem (保存和比较内存)**](-holdmem--hold-and-compare-memory-.md)命令将一个内存范围与另一个内存范围进行比较。

在大多数情况下，这些命令会在当前基数中解释它们的参数。 因此，如果当前基数不为16，则应在十六进制地址前面添加 **0x** 。 但是，无论当前基数如何，这些命令的显示输出通常采用十六进制格式。  (有关输出的详细信息，请参阅各个命令主题。 ) [内存窗口](memory-window.md) 显示十进制格式的整数和实数，并以十六进制格式显示其他格式。

若要更改默认基数，请使用 [**n (设置 Number Base)**](n--set-number-base-.md) 命令。 若要快速地将数字从一个基转换到另一个基，请使用 [**？ (计算 Expression)**](---evaluate-expression-.md) 命令或 [**. formats () 命令显示数字格式**](-formats--show-number-formats-.md) 。

执行用户模式调试时，虚拟地址的含义由当前进程确定。 执行内核模式调试时，调试器可以控制虚拟地址的含义。 有关详细信息，请参阅 [处理上下文](changing-contexts.md#process-context)。

 

 





