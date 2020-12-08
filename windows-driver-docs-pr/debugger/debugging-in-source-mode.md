---
title: 在源模式下调试
description: 在源模式下调试
keywords:
- 源调试
- 源模式
- 源代码调试，概述
- '构建实用程序 ( # A0) ，避免优化'
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e0f58ea7cd3ccbff223f60d02b41b422e9d9937
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817541"
---
# <a name="debugging-in-source-mode"></a>在源模式下调试


## <span id="ddk_debugging_in_source_mode_dbg"></span><span id="DDK_DEBUGGING_IN_SOURCE_MODE_DBG"></span>


如果可以分析代码源而不是反汇编的二进制文件，调试应用程序会更容易。

如果源语言是 C、c + + 或程序集，则 WinDbg、CDB 和 KD 可以使用调试中的源代码。

### <a name="span-idcompilation_requirementsspanspan-idcompilation_requirementsspancompilation-requirements"></a><span id="compilation_requirements"></span><span id="COMPILATION_REQUIREMENTS"></span>编译要求

若要使用源调试，您必须在生成二进制文件时，您的编译器或链接器 ( .pdb 文件) 创建符号文件。 这些符号文件显示调试器如何与源行相对应的二进制说明。

此外，由于符号文件不包含实际源文本，因此调试器必须能够访问实际的源文件。

如果可能，编译器和链接器不应优化代码。 如果代码已经过优化，则源调试和对本地变量的访问更难，有时可能几乎不可能。 如果使用生成实用工具作为编译器和链接器，请将 MSC \_ 优化宏设置为 **/od/Oi** 以避免优化。

### <a name="span-idlocating_the_symbol_files_and_source_filesspanspan-idlocating_the_symbol_files_and_source_filesspanlocating-the-symbol-files-and-source-files"></a><span id="locating_the_symbol_files_and_source_files"></span><span id="LOCATING_THE_SYMBOL_FILES_AND_SOURCE_FILES"></span>查找符号文件和源文件

若要在源模式下进行调试，调试器必须能够找到源文件和符号文件。 有关详细信息，请参阅 [源代码](source-code.md)。

### <a name="span-idbeginning_source_debuggingspanspan-idbeginning_source_debuggingspanbeginning-source-debugging"></a><span id="beginning_source_debugging"></span><span id="BEGINNING_SOURCE_DEBUGGING"></span>开始源调试

每当调试程序具有用于当前正在调试的线程的正确符号和源文件时，调试器都可以显示源信息。

如果使用调试器启动新的用户模式应用程序，则在 Ntdll.dll 加载该应用程序时，将发生初始中断。 由于调试器无法访问 Ntdll.dll 的源文件，此时无法访问应用程序的源信息。

若要将程序计数器移到应用程序的开始位置，请在二进制文件的入口点处添加断点。 在 [命令窗口的调试器](debugger-command-window.md)中，键入以下命令。

```dbgcmd
bp main
g
```

然后，在输入 **main** 函数时，将加载并停止应用程序。 当然， (可以使用任何入口点，而不是只使用 **main**。 ) 

如果应用程序引发异常，则会中断调试器。 此时提供源信息。 但是，如果您使用 [**ctrl + C**](ctrl-c--break-.md)、 [ctrl + break](debug---break.md)或 Debug 发出了中断 |Break 命令，调试器会创建一个新线程，因此看不到源代码。

到达具有的源文件的线程后，可以使用调试器命令窗口执行源调试命令。 如果使用的是 WinDbg，则会显示 [源窗口](source-window.md) 。 如果已通过单击 "**文件**" 菜单上的 "**打开源文件**" 打开了源窗口，则 WinDbg 通常会为源创建新窗口。 你可以在不影响调试过程的情况下关闭上一个窗口。

### <a name="span-idsource_debugging_in_the_windbg_guispanspan-idsource_debugging_in_the_windbg_guispansource-debugging-in-the-windbg-gui"></a><span id="source_debugging_in_the_windbg_gui"></span><span id="SOURCE_DEBUGGING_IN_THE_WINDBG_GUI"></span>WinDbg GUI 中的源调试

如果使用的是 WinDbg，则只要程序计数器包含在调试器中包含其源信息的代码中，就会显示源窗口。

WinDbg 为你或 WinDbg 打开的每个源文件显示一个源窗口。 有关此窗口的文本属性的详细信息，请参阅 [源窗口](source-window.md)。

然后，可以单步执行应用程序或执行到断点或游标。 有关单步执行和跟踪命令的详细信息，请参阅 [控制目标](controlling-the-target.md)。

如果处于源模式，则在单步执行应用程序时，相应的源窗口会移动到前台。 由于还会在应用程序执行过程中调用 Microsoft Windows 例程，因此当发生这种调用时，调试程序可能会将 " [反汇编" 窗口](disassembly-window.md) 移动到前台 (因为调试器没有) 的这些函数的源的访问权限。 当程序计数器返回到已知源文件时，相应的源窗口将变为活动状态。

当你在应用程序中移动时，WinDbg 会在源窗口和 "反汇编" 窗口中突出显示你的位置。 还将突出显示设置了断点的行。 根据语言的分析来着色源代码。 如果已选择 "源" 窗口，则可以使用鼠标将鼠标悬停在符号上，以便对其进行计算。 有关这些功能以及如何控制这些功能的详细信息，请参阅 [源窗口](source-window.md)。

若要在 WinDbg 中激活源模式，请使用 " [**+ t**](l---l---set-source-options-.md) " 命令，单击 "**调试**" 菜单上的 "**源模式**"，或单击工具栏上的 "源模式的源模式 (屏幕截图 **" 按钮** ![ ](images/tbsrc.png)) 。

当源模式处于活动状态时， **ASM** 指示器在状态栏上显示为不可用。

在源模式下逐句通过函数时，可以查看或更改任何本地变量的值。 有关详细信息，请参阅 [读取和写入内存](reading-and-writing-memory.md)。

### <a name="span-idsource_debugging_in_the_debugger_command_windowspanspan-idsource_debugging_in_the_debugger_command_windowspansource-debugging-in-the-debugger-command-window"></a><span id="source_debugging_in_the_debugger_command_window"></span><span id="SOURCE_DEBUGGING_IN_THE_DEBUGGER_COMMAND_WINDOW"></span>调试器命令窗口中的源调试

如果使用的是 CDB，则没有单独的源窗口。 不过，您仍可以在逐句浏览源时查看进度。

在 CDB 中进行源调试之前，必须通过发出 [**lines (切换源代码行支持)**](-lines--toggle-source-line-support-.md) 命令或通过使用 [**-line 命令行选项**](cdb-command-line-options.md)启动调试器来加载源行符号。

如果执行 [**l + t**](l---l---set-source-options-.md) 命令，所有程序单步执行一次会执行一个源行。 使用 **l-t** 一次单步执行一个程序集指令。 如果使用的是 WinDbg，则此命令的作用与在 "**调试**" 菜单上选择或清除 **源模式** 或使用工具栏按钮相同。

[**L + s**](l---l---set-source-options-.md)命令在提示符处显示当前的源行和行号。 如果只想查看行号，请改用 **l + l** 。

如果使用 [**l + o**](l---l---set-source-options-.md) 和 **l + s**，则在逐句通过程序时只显示源行。 隐藏程序计数器、反汇编代码和注册信息。 利用这种显示，您可以快速单步执行代码，并查看源以外的任何内容。

您可以使用 [**lsp (设置源行数)**](lsp--set-number-of-source-lines-.md) 命令来指定在单步执行或执行应用程序时确切显示多少源行。

下面的命令顺序是单步执行源文件的有效方法。

```text
.lines        enable source line information
bp main       set initial breakpoint
l+t           stepping will be done by source line
l+s           source lines will be displayed at prompt
g             run program until "main" is entered
pr            execute one source line, and toggle register display off
p             execute one source line 
```

因为 [**ENTER**](enter--repeat-last-command-.md) 重复了最后一个命令，所以现在可以使用 ENTER 键单步执行应用程序。 每个步骤都会导致显示源行、内存偏移量和程序集代码。

有关如何解释反汇编显示的详细信息，请参阅 [在程序集模式下进行调试](debugging-in-assembly-mode.md)。

当显示程序集代码时，正在访问的任何内存位置都显示在该行的右端。 您可以使用 [**d \* (显示内存)**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md) 和 [**e \* (输入值)**](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md) 命令来查看或更改这些位置中的值。

如果必须查看每个程序集指令以确定偏移或内存信息，请使用 [**l t**](l---l---set-source-options-.md) 按程序集指令（而不是源行）单步执行。 源行信息仍可显示。 每个源行对应一个或多个程序集指令。

所有这些命令都在 WinDbg 和 CDB 中可用。 您可以使用命令来查看 WinDbg 的 [调试器命令窗口](debugger-command-window.md) 而不是源窗口中的源行信息。

### <a name="span-idsource_lines_and_offsetsspanspan-idsource_lines_and_offsetsspansource-lines-and-offsets"></a><span id="source_lines_and_offsets"></span><span id="SOURCE_LINES_AND_OFFSETS"></span>源行和偏移量

还可以使用表达式计算器来执行源调试，以确定对应于特定源行的偏移量。

以下命令显示内存偏移量。

```dbgcmd
? `[[module!]filename][:linenumber]` 
```

如果省略 *filename*，则调试器会搜索与当前程序计数器相对应的源文件。

除非当前的默认基数，否则调试器会将 *linenumber* 读取为十进制数，除非在它之前添加 **0x** 。 如果省略 *linenumber*，则表达式的计算结果为对应于源文件的可执行文件的初始地址。

仅当 **lines** 命令或 **行** 命令行选项加载了源行符号时，才会在 CDB 中理解此语法。

此方法的用途非常广泛，因为无论程序计数器指向何处，都可以使用它。 例如，利用此方法，您可以通过使用如下所示的命令提前设置断点。

```dbgcmd
bp `source.c:31` 
```

有关详细信息，请参阅 [源行语法](source-line-syntax.md) 和 [使用断点](using-breakpoints.md)。

### <a name="span-idstepping_and_tracing_in_source_modespanspan-idstepping_and_tracing_in_source_modespanstepping-and-tracing-in-source-mode"></a><span id="stepping_and_tracing_in_source_mode"></span><span id="STEPPING_AND_TRACING_IN_SOURCE_MODE"></span>源模式下的单步执行和跟踪

在源模式下进行调试时，单个源行上可以有多个函数调用。 不能使用 **p** 和 **t** 命令来分隔这些函数调用。

例如，在下面的命令中， **t** 命令单步执行 **GetTickCount** 和 **printf**，而 **p** 命令执行两个函数调用的步骤。

```cpp
printf( "%x\n", GetTickCount() );
```

如果你想要在跟踪到其他调用时单步执行某些调用，请使用 [**。步骤 \_ 筛选器 (设置步骤筛选器)**](-step-filter--set-step-filter-.md) ，以指示要逐过程的调用。

您可以使用 **\_ 步骤 \_ 筛选** 器筛选出框架函数 (例如，MICROSOFT 基础类 (MFC) 或活动模板库 (ATL) 调用) 。

 

 





