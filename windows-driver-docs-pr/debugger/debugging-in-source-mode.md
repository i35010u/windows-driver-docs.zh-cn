---
title: 在源模式下调试
description: 在源模式下调试
ms.assetid: b236f53b-2429-4085-b008-6648d1474ec2
keywords:
- 源调试
- 源模式
- 源调试概述
- 生成实用工具 (build.exe) 避免优化
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0264517c0956a00dee2d59cff3c17078856963b0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350606"
---
# <a name="debugging-in-source-mode"></a>在源模式下调试


## <span id="ddk_debugging_in_source_mode_dbg"></span><span id="DDK_DEBUGGING_IN_SOURCE_MODE_DBG"></span>


调试应用程序是代码的可以分析，而不是代码的已拆装的二进制文件的源的情况下更轻松。

WinDbg、 CDB 和 KD 可以使用源代码在调试中，如果源语言为 C， C++，或程序集。

### <a name="span-idcompilationrequirementsspanspan-idcompilationrequirementsspancompilation-requirements"></a><span id="compilation_requirements"></span><span id="COMPILATION_REQUIREMENTS"></span>编译需求

若要使用源代码调试，必须具有编译器或链接器创建符号文件 （.pdb 文件） 时生成二进制文件。 这些符号文件显示在调试器的二进制说明如何与源行相对应。

此外，调试器必须能够访问实际的源文件，因为符号文件不包含实际源文本。

如果可能，编译器和链接器不应优化你的代码。 源调试和本地变量的访问权限是更困难，并且有时几乎不可能，如果代码已经过优化。 如果使用的生成实用工具作为你的编译器和链接器，设置 MSC\_到优化宏 **/Od /Oi**以免优化。

### <a name="span-idlocatingthesymbolfilesandsourcefilesspanspan-idlocatingthesymbolfilesandsourcefilesspanlocating-the-symbol-files-and-source-files"></a><span id="locating_the_symbol_files_and_source_files"></span><span id="LOCATING_THE_SYMBOL_FILES_AND_SOURCE_FILES"></span>查找符号文件和源文件

若要调试在源文件模式下，调试器必须能够找到的源文件和符号文件。 有关详细信息，请参阅[源代码](source-code.md)。

### <a name="span-idbeginningsourcedebuggingspanspan-idbeginningsourcedebuggingspanbeginning-source-debugging"></a><span id="beginning_source_debugging"></span><span id="BEGINNING_SOURCE_DEBUGGING"></span>从开始源调试

只要它具有正确的符号和源代码文件的线程的当前正在调试，调试器可以显示源信息。

如果您使用调试器启动一个新的用户模式应用程序，初始在中断发生时 Ntdll.dll 加载应用程序。 因为调试器不具有到 Ntdll.dll 源代码文件的访问权限，无法访问你的应用程序此时源信息。

若要移动的程序计数器到应用程序的开头，请为你的二进制文件在入口点添加断点。 在中[调试器命令窗口](debugger-command-window.md)，键入以下命令。

```dbgcmd
bp main
g
```

应用程序随后被加载并停止**主要**输入函数。 (当然，您可以使用任何入口点，而不仅仅**主要**。)

如果应用程序引发了异常，它会中断到调试器。 在这里提供了源信息。 但是，如果通过使用发出一个分行符[ **CTRL + C**](ctrl-c--break-.md)， [CTRL + BREAK](debug---break.md)，或调试 |换行命令，调试器创建一个新线程，因此不能看到你的源代码。

你已达到源文件包含一个线程后，可以使用调试器命令窗口执行调试命令的源。 如果使用的 WinDbg 中，[源窗口](source-window.md)出现。 如果已打开源窗口中单击**打开源文件**上**文件**菜单中，WinDbg 通常创建新的窗口的源。 而不会影响调试的过程，可以关闭上一个窗口。

### <a name="span-idsourcedebugginginthewindbgguispanspan-idsourcedebugginginthewindbgguispansource-debugging-in-the-windbg-gui"></a><span id="source_debugging_in_the_windbg_gui"></span><span id="SOURCE_DEBUGGING_IN_THE_WINDBG_GUI"></span>源在 WinDbg GUI 中进行调试

如果使用 WinDbg，只要程序计数器是调试器具有源信息的代码中会出现在源窗口。

WinDbg 显示每个打开您或 WinDbg 的源文件的一个源窗口。 有关此窗口的文本属性的详细信息，请参阅[源 Windows](source-window.md)。

然后可以单步执行您的应用程序或执行到断点或光标。 有关单步执行和跟踪命令的详细信息，请参阅[控制目标](controlling-the-target.md)。

如果要在源模式中，单步执行您的应用程序在相应的源窗口将移到前台。 由于还没有 Microsoft Windows 应用程序的执行期间调用的例程，调试器可能会将移动[反汇编窗口](disassembly-window.md)到前台，这种调用时 （因为调试器不具有访问到这些函数的源）。 当程序计数器返回到已知的源文件时，在相应的源窗口将变为活动状态。

当你移动通过应用程序，WinDbg 突出显示了你在源窗口和反汇编窗口中的位置。 设置断点的行也会突出显示。 根据语言的分析进行着色的源代码。 如果已选择源窗口中，你可以悬停符号上，以对其进行评估。 有关这些功能以及如何控制它们的详细信息，请参阅[源 Windows](source-window.md)。

若要激活源模式在 WinDbg 中的，使用[ **l + t** ](l---l---set-source-options-.md)命令，请单击**源模式**上**调试**菜单上或单击**在源模式**按钮 (![按钮上的源模式的屏幕截图](images/tbsrc.png)) 工具栏上。

源模式处于活动状态时**ASM**指示器将显示在状态栏上不可用。

在可以查看或更改任何本地变量的值，在逐步执行源模式中的函数。 有关详细信息，请参阅[读取和写入内存](reading-and-writing-memory.md)。

### <a name="span-idsourcedebugginginthedebuggercommandwindowspanspan-idsourcedebugginginthedebuggercommandwindowspansource-debugging-in-the-debugger-command-window"></a><span id="source_debugging_in_the_debugger_command_window"></span><span id="SOURCE_DEBUGGING_IN_THE_DEBUGGER_COMMAND_WINDOW"></span>源在调试器命令窗口中进行调试

如果使用 CDB，您没有单独的源窗口。 但是，在逐步执行源仍可以查看您的进度。

你可以先执行源在 CDB 中进行调试，则必须通过发出加载源行符号[ **.lines （切换源行支持）** ](-lines--toggle-source-line-support-.md)命令，或通过启动的调试器中[ **的行命令行选项**](cdb-command-line-options.md)。

如果您执行[ **l + t** ](l---l---set-source-options-.md)命令时，单步执行的所有程序执行一个源行一次。 使用**l-t**以步骤一次一个程序集指令。 如果使用 WinDbg，此命令具有相同的效果选中或清除**源模式**上**调试**菜单或使用工具栏按钮。

[ **L + s** ](l---l---set-source-options-.md)命令在提示符下显示的当前源行和行号。 如果想要查看仅行号，使用**l + l**相反。

如果您使用[ **l + o** ](l---l---set-source-options-.md)并**l + s**，仅源行显示，而单步执行程序。 隐藏程序计数器、 反汇编代码和寄存器信息。 这种类型的显示，可快速单步执行代码并查看执行任何操作但源。

可以使用[ **lsp （设置源行数）** ](lsp--set-number-of-source-lines-.md)命令，指定单步执行或执行应用程序时，完全显示源行数。

下面的命令序列是逐步执行源文件的有效方法。

```text
.lines        enable source line information
bp main       set initial breakpoint
l+t           stepping will be done by source line
l+s           source lines will be displayed at prompt
g             run program until "main" is entered
pr            execute one source line, and toggle register display off
p             execute one source line 
```

因为[ **ENTER** ](enter--repeat-last-command-.md)重复最后一个命令，现在可以通过使用 ENTER 键逐句通过应用程序。 每个步骤会导致在源行、 内存偏移量和程序集代码才会显示。

有关如何解释反汇编显示的详细信息，请参阅[在程序集模式下调试](debugging-in-assembly-mode.md)。

显示程序集代码时，行的右端显示正在访问任何内存位置。 可以使用[ **d\* （显示内存）** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)并[ **e\* （输入值）** ](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md)命令以查看或更改这些位置中的值。

如果您需要查看每个程序集指令来确定的偏移量或使用的内存信息[ **l-t** ](l---l---set-source-options-.md)到步骤而不是源行的程序集指令。 仍将显示源代码行信息。 每个源行对应于一个或多个程序集指令。

所有这些命令都在 WinDbg 和 CDB 中可用。 可以使用命令来查看从 WinDbg 的源代码行信息[调试器命令窗口](debugger-command-window.md)而不是从源窗口。

### <a name="span-idsourcelinesandoffsetsspanspan-idsourcelinesandoffsetsspansource-lines-and-offsets"></a><span id="source_lines_and_offsets"></span><span id="SOURCE_LINES_AND_OFFSETS"></span>源行和偏移量

此外可以使用表达式计算器来确定对应于特定的源行的偏移量进行调试的源。

下面的命令显示内存偏移量。

```dbgcmd
? `[[module!]filename][:linenumber]` 
```

如果省略*文件名*，调试器搜索源文件对应于当前的程序计数器。

调试器读取*linenumber*为十进制数字除非添加**0x**之前它，而不考虑当前的默认基数。 如果省略*linenumber*，表达式的计算结果与源文件相对应的可执行文件的初始地址。

此语法识别的 CDB 才 **.lines**命令或 **-行**命令行选项已加载源行符号。

此技术是非常通用，因为可以使用它而不考虑其中指向程序计数器。 例如，此技术，可使用如下所示的命令，请提前设置断点。

```dbgcmd
bp `source.c:31` 
```

有关详细信息，请参阅[源行语法](source-line-syntax.md)并[使用断点](using-breakpoints.md)。

### <a name="span-idsteppingandtracinginsourcemodespanspan-idsteppingandtracinginsourcemodespanstepping-and-tracing-in-source-mode"></a><span id="stepping_and_tracing_in_source_mode"></span><span id="STEPPING_AND_TRACING_IN_SOURCE_MODE"></span>单步执行和在源模式中进行跟踪

在源模式中调试时，单个源行上可以有多个函数调用。 不能使用**p**并**t**命令来分隔这些函数调用。

例如，在以下命令， **t**命令到步骤**GetTickCount**并**printf**，而**p**逐过程执行命令这两个函数调用。

```cpp
printf( "%x\n", GetTickCount() );
```

如果你想要通过特定的调用跟踪时单步执行其他调用，使用[**步骤\_筛选器 （设置步骤筛选器）** ](-step-filter--set-step-filter-.md)以指示它通过调用到步骤。

可以使用**\_步骤\_筛选器**若要筛选出框架函数 （例如，Microsoft 基础类 (MFC) 或活动模板库 (ATL) 调用）。

 

 





