---
title: 在程序集模式下调试
description: 在程序集模式下调试
keywords:
- 程序集调试
- 程序集模式
- 程序集调试，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: da0b47c6940254dd298520ffaa61b638ae85c4b7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817545"
---
# <a name="debugging-in-assembly-mode"></a>在程序集模式下调试


## <span id="ddk_debugging_in_assembly_mode_dbg"></span><span id="DDK_DEBUGGING_IN_ASSEMBLY_MODE_DBG"></span>


如果你的应用程序具有 C 或 c + + 源文件，则如果 [在源模式下进行调试](debugging-in-source-mode.md)，则可以使用该调试器更多有效。

但在许多情况下，不能执行源调试。 你可能没有应用程序的源文件。 您可能正在调试其他人的代码。 你可能没有使用完整 .pdb 符号生成可执行文件。 即使您可以在您的应用程序上执行源调试，您可能也需要跟踪您的应用程序所调用的或用于加载您的应用程序的 Microsoft Windows 例程。

在这些情况下，必须在程序集模式下进行调试。 而且，程序集模式包含许多在源调试中不存在的有用功能。 调试器会自动显示内存位置的内容，并在访问时注册，并显示程序计数器的地址。 此显示使程序集调试成为一个非常有用的工具，您可以将这些工具与源调试一起使用。

### <a name="span-iddisassembly_codespanspan-iddisassembly_codespandisassembly-code"></a><span id="disassembly_code"></span><span id="DISASSEMBLY_CODE"></span>反汇编代码

调试器主要分析二进制可执行代码。 调试器会 *反汇编* 此代码，而不是以 raw 格式显示此代码。 也就是说，调试器会将代码从计算机语言转换为汇编语言。

可以通过几种不同的方式将生成的代码 (称为 *反汇编代码*) ：

-   [**U (Unassemble)**](u--unassemble-.md)命令反汇编并显示计算机语言的指定部分。

-   [**Uf (Unassemble 函数)**](uf--unassemble-function-.md)命令反汇编并显示函数。

-   [**向上 (Unassemble 的物理内存)**](up--unassemble-from-physical-memory-.md)命令反汇编，并显示已存储在物理内存中的计算机语言指定部分。

-   [**(Unassemble 实模式 BIOS)**](ur--unassemble-real-mode-bios-.md)命令反汇编并显示指定的16位实模式代码。

-   [**Ux (Unassemble X86 BIOS)**](ux--unassemble-x86-bios-.md)命令反汇编并显示指定地址处基于 X86 的 bios 代码指令集。

-    (WinDbg 仅) " [反汇编" 窗口](view---disassembly.md) 反汇编并显示计算机语言的指定部分。 如果您在 "**窗口**" 菜单中选择 "**自动打开反汇编**" 命令，此窗口将自动处于活动状态。 还可以通过在 "**视图**" 菜单上选择 "**反汇编**"，按 alt + 7，或按 "**反汇编" (alt + 7)** "按钮， (在 ![ WinDbg 工具栏上的" 反汇编 "按钮) 屏幕截图 ](images/tbdisasm2.png) 。

反汇编显示在四列中：地址偏移量、二进制代码、程序集语言助记键和程序集语言详细信息。 下面的示例演示了这种显示。

```dbgcmd
0040116b    45          inc         ebp            
0040116c    fc          cld                        
0040116d    8945b0      mov         eax,[ebp-0x1c] 
```

在表示当前程序计数器的行的右侧，显示的将显示正在访问的任何内存位置或寄存器的值。 如果此行包含分支指令，则显示表示法 " **\[ br = \] 1** " 或 " **\[ br = 0 \]** "。 此表示法表示每个分支都是或。

您可以使用 [**.asm (更改反汇编选项)**](-asm--change-disassembly-options-.md) 命令更改反汇编说明的显示方式。

在 WinDbg 的 "反汇编" 窗口中，将突出显示表示当前程序计数器的行。 还将突出显示断点所在的行。

你还可以使用以下命令来操作程序集代码：

-   [**\# (搜索反汇编模式)**](---search-for-disassembly-pattern-.md)命令在内存区域中搜索特定模式。 此命令等效于搜索显示的四列反汇编。

-   [**(汇编)**](a--assemble-.md)命令可以获取程序集指令并将它们转换为二进制计算机代码。

### <a name="span-idassembly_mode_and_source_modespanspan-idassembly_mode_and_source_modespanassembly-mode-and-source-mode"></a><span id="assembly_mode_and_source_mode"></span><span id="ASSEMBLY_MODE_AND_SOURCE_MODE"></span>程序集模式和源模式

调试器具有两个不同的运行模式： *程序集模式* 和 *源模式*。

如果是单步执行应用程序，则单个步骤的大小为一个程序集代码行，或一个源代码行（具体取决于模式）。

根据模式，会显示多个命令创建不同的数据。

在 WinDbg 中，当你在程序集模式下运行或单步执行应用程序时，" [反汇编" 窗口](disassembly-window.md) 将自动移到前台。 在源模式下， [源窗口](source-window.md) 移到前台。

若要设置模式，可以执行以下操作之一：

-   使用 [**l +，l- (Set Source Options)**](l---l---set-source-options-.md) 命令来控制模式。 **L t** 命令激活程序集模式。

-    (WinDbg 仅) 清除 "**调试**" 菜单上的 "**源模式**" 命令，使调试器进入程序集模式。你还可以在工具栏上的 "源模式关闭") 按钮 (屏幕截图中，选择 "**关闭源模式**" 按钮 ![ ](images/tbasm.png) 。

在 WinDbg 中，当处于程序集模式时， **ASM** 显示在状态栏上。

WinDbg 的 "反汇编" 窗口中的快捷菜单包括 " **当前源代码行" 命令中的突出显示说明** 。 此命令将突出显示与当前源行对应的所有说明。 通常，单个源行对应于多个程序集指令。 如果代码已经过优化，则这些程序集指令可能不是连续的。 **通过 "当前源代码行" 命令中的突出显示说明**，您可以找到从当前源行收集的所有说明。

### <a name="span-idassembly_language_source_filesspanspan-idassembly_language_source_filesspanassembly-language-source-files"></a><span id="assembly_language_source_files"></span><span id="ASSEMBLY_LANGUAGE_SOURCE_FILES"></span>汇编语言源文件

如果你的应用程序是以汇编语言编写的，则调试器生成的反汇编可能与原始代码不完全匹配。 具体而言，NO-OPs 和注释不会出现。

如果要通过引用原始 .asm 文件来调试代码，则必须使用源模式调试。 可以加载程序集文件，如 C 或 c + + 源文件。 有关此类调试的详细信息，请参阅 [源模式下的调试](debugging-in-source-mode.md)。

 

 





