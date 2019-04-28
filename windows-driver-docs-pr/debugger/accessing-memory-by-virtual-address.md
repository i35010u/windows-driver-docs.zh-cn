---
title: 按虚拟地址访问内存
description: 按虚拟地址访问内存
ms.assetid: 13e97cba-c4a4-4240-99b3-88a7537b0ca8
keywords:
- 访问内存的虚拟地址
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3610080427c4c3ec3defce989d4689e994690468
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351487"
---
# <a name="accessing-memory-by-virtual-address"></a>按虚拟地址访问内存


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


若要访问的内存地址或地址范围，可以使用多个命令。 Visual Studio 和 WinDbg 提供用户界面元素 （以及命令） 可用于查看和编辑内存。 有关详细信息，请参阅[查看和编辑内存和 Visual Studio 中的寄存器](viewing-memory--variables--and-registers-in-visual-studio.md)并[查看和编辑内存在 WinDbg 中](memory-window.md)。

以下命令可读取或写入内存中以不同的格式。 这些格式包括十六进制字节、 字 （单词、 双字和四字）、 （短、 长时间，与四整数和无符号的整数） 的整数、 浮点数 （10 字节、 16 个字节，32 位和 64 字节实数） 和 ASCII 字符。

-   [ **D\* （显示内存）** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令显示指定的内存地址或范围的内容。

-   [ **E\* （输入值）** ](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md)命令将值写入指定的内存地址。

可以使用以下命令来处理更专用的数据类型：

-   [ **Dt （显示类型）** ](dt--display-type-.md)命令查找各种数据类型，并显示已由正在调试的应用程序创建的数据结构。 此命令是高度通用且具有许多变体和选项。

-   [ **Ds，dS （显示字符串）** ](ds--ds--display-string-.md)命令显示的字符串，ANSI\_字符串或 UNICODE\_字符串数据结构。

-   [ **Dl （显示链接列表）** ](dl--display-linked-list-.md)命令跟踪，并显示链接的列表。

-   [ **D\*s （显示单词和符号）** ](dds--dps--dqs--display-words-and-symbols-.md)命令查找双字或四字可能包含符号信息并显示数据和符号信息。

-   [ **！ 地址**](-address.md)扩展命令将显示位于特定地址的内存的属性信息。

可以使用以下命令来处理内存范围：

-   [ **M （移动内存）** ](m--move-memory-.md)命令将一个内存范围的内容移动到另一个。

-   [ **F （填充内存）** ](f--fp--fill-memory-.md)命令写入到内存范围，一种模式写下去，直到该区域已满。

-   [ **C （比较内存）** ](c--compare-memory-.md)命令将比较两个内存范围的内容。

-   [ **S （内存搜索）** ](s--search-memory-.md)命令内存范围内的指定模式搜索或内存区域中存在任何 ASCII 或 Unicode 字符的搜索。

-   [ **.Holdmem （保留和比较内存）** ](-holdmem--hold-and-compare-memory-.md)命令将到另一个内存范围进行比较。

在大多数情况下，这些命令将解释它们当前基数的参数。 因此，应添加**0x**之前十六进制的地址，如果当前的基数不是 16。 但是，这些命令显示输出通常是以十六进制格式，而不考虑当前的基数。 （有关输出的详细信息，请参阅单个命令主题）。[内存窗口](memory-window.md)以十进制格式显示整数和实数，并以十六进制格式显示其他格式。

若要更改默认基数，请使用[ **n (设置数量 Base)** ](n--set-number-base-.md)命令。 若要快速将数字从一个基转换为另一个，请使用[ **？（计算表达式）** ](---evaluate-expression-.md)命令或[ **.formats （显示数字格式）** ](-formats--show-number-formats-.md)命令。

当您在执行用户模式下调试时，由当前进程确定虚拟地址的含义。 当您在执行内核模式调试时，可通过调试器控制虚拟地址的含义。 有关详细信息，请参阅[进程上下文](changing-contexts.md#process-context)。

 

 





