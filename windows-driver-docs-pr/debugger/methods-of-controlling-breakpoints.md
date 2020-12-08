---
title: 断点控制方法
description: 断点控制方法
keywords:
- 断点，控制
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf737ec9f86be23cf4e9074a8a78d32ee41d5d8c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814527"
---
# <a name="methods-of-controlling-breakpoints"></a>断点控制方法


在源模式) 时，可以按虚拟地址、模块和例程偏移量或源文件和行号指定断点的位置 (。 如果在没有偏移量的例程上放置断点，则在输入该例程时会激活该断点。

还有几种其他类型的断点：

-   断点可以与某个线程关联。

-   断点可以在触发之前通过地址启用固定数量的传递。

-   断点可以在触发时自动发出某些命令。

-   可对不可执行的内存设置断点，并监视要读取或写入的位置。

如果要在用户模式中调试多个进程，断点的集合取决于当前进程。 若要查看或更改进程的断点，您必须选择进程作为当前进程。 有关当前进程的详细信息，请参阅 [控制进程和线程](controlling-processes-and-threads.md)。

### <a name="span-idmethods_of_controlling_and_displaying_breakpointsspanspan-idmethods_of_controlling_and_displaying_breakpointsspandebugger-commands-for-controlling-and-displaying-breakpoints"></a><span id="methods_of_controlling_and_displaying_breakpoints"></span><span id="METHODS_OF_CONTROLLING_AND_DISPLAYING_BREAKPOINTS"></span>用于控制和显示断点的调试器命令

若要控制或显示断点，可以使用以下方法：

-   使用 [**bl (断点列表)**](bl--breakpoint-list-.md) 命令列出现有断点及其当前状态。

-   使用 [**bpcmds (显示断点命令)**](-bpcmds--display-breakpoint-commands-.md) 命令，列出所有断点以及用于创建断点的命令。

-   使用 [**bp (设置断点)**](bp--bu--bm--set-breakpoint-.md) 命令设置新断点。

-   使用 [**bu (设置未解析的断点)**](bp--bu--bm--set-breakpoint-.md) 命令设置新断点。 用 **bu** 设置的断点称为未解析的断点;它们的特征不同于使用 **bp** 设置的断点。 有关完整的详细信息，请参阅 [)  (Bu 断点的未解析断点 ](unresolved-breakpoints---bu-breakpoints-.md)。

-   使用 [**bm.exe (设置符号断点)**](bp--bu--bm--set-breakpoint-.md) 命令设置与指定模式匹配的符号上的新断点。 使用 **bm.exe** 设置的断点将与一个地址 (如 **bp** 断点一样) 如果包含 **/d** 开关，则为; 否则为。如果不包含此开关，它将不能解析 (如 **bu** 断点) 。

-   使用 " [**ba (访问) "**](ba--break-on-access-.md) 命令设置 *处理器断点*（也称为 *数据断点*）。 当写入内存位置时、读取时、作为代码执行或发生内核 i/o 时，可以触发这些断点。 有关完整的详细信息，请参阅 [ (Ba 断点) 处理器断点 ](processor-breakpoints---ba-breakpoints-.md)。

-   使用 " [**bc (" 断点清除)**](bc--breakpoint-clear-.md) "命令以永久删除一个或多个断点。

-   使用 " [**bd (" 断点禁用)**](bd--breakpoint-disable-.md) 命令，以暂时禁用一个或多个断点。

-   使用 " [**(" 断点启用)**](be--breakpoint-enable-.md) 命令，以重新启用一个或多个禁用的断点。

-   使用 " [**br" ("断点对)**](br--breakpoint-renumber-.md) 命令进行重新编号，以更改现有断点的 ID。

-   使用 [**bs.1770 (Update 断点命令)**](bs--update-breakpoint-command-.md) 命令更改与现有断点关联的命令。

-   使用 " [**.bsc (更新条件断点")**](bsc--update-conditional-breakpoint-.md) 命令更改现有条件断点的发生条件。

在 Visual Studio 和 WinDbg 中，有多个用户界面元素可帮助控制和显示断点。 请参阅 [在 Visual Studio 中设置断点](setting-breakpoints-in-visual-studio.md) 和 [在 WinDbg 中设置断点](setting-breakpoints-in-windbg.md)。

每个断点都有一个十进制数，称为与之关联的断点 ID。 此数字标识多个命令中的断点。

### <a name="span-idbreakpoint_commandsspanspan-idbreakpoint_commandsspanbreakpoint-commands"></a><span id="breakpoint_commands"></span><span id="BREAKPOINT_COMMANDS"></span>断点命令

可以将命令包含在命中断点时自动执行的断点中。 例如，以下命令在 MyFunction + 0x47 处中断，写入一个转储文件，然后继续执行。

```dbgcmd
0:000> bu MyFunction+0x47 ".dump c:\mydump.dmp; g" 
```

**注意**  如果要从内核调试器控制用户模式调试器，请不要在断点命令字符串中使用 [**g (中转)**](g--go-.md) 。 串行接口可能无法跟上此命令，您将无法返回到 CDB。 有关此情况的详细信息，请参阅 [从内核调试器控制 User-Mode 调试器](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)。

 

### <a name="span-idnumber_of_breakpointsspanspan-idnumber_of_breakpointsspannumber-of-breakpoints"></a><span id="number_of_breakpoints"></span><span id="NUMBER_OF_BREAKPOINTS"></span>断点数

在内核模式下，最多可以使用32个软件断点。 在用户模式下，可以使用任意数量的软件断点。

支持的处理器断点数取决于目标处理器的体系结构。

### <a name="span-idconditional_breakpointsspanspan-idconditional_breakpointsspanconditional-breakpoints"></a><span id="conditional_breakpoints"></span><span id="CONDITIONAL_BREAKPOINTS"></span>条件断点

可以设置仅在特定条件下触发的断点。 有关这些类型断点的详细信息，请参阅 [设置条件断点](setting-a-conditional-breakpoint.md)。

 

 





