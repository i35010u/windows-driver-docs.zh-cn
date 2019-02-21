---
title: 在程序集模式中进行调试
description: 在程序集模式中进行调试
ms.assetid: 048c43ff-7f9e-4a20-a524-44f66d92eefe
keywords:
- 调试的程序集
- 程序集模式
- 程序集调试概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78107ec7196f9948dddecd85dd12458c01a14347
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522806"
---
# <a name="debugging-in-assembly-mode"></a>在程序集模式中进行调试


## <span id="ddk_debugging_in_assembly_mode_dbg"></span><span id="DDK_DEBUGGING_IN_ASSEMBLY_MODE_DBG"></span>


如果您应用程序具有 C 或 c + + 源文件，则可以使用调试器功能非常强大得多如果您[在源模式下调试](debugging-in-source-mode.md)。

但是，有很多时候，不能执行源调试。 不可能适用于你的应用程序的源文件。 您可以调试其他人的代码。 您可能不生成完整的.pdb 符号与可执行文件。 即使你可以执行源在你的应用程序上进行调试，则可能必须跟踪 Microsoft Windows 例程应用程序应调用或使用以加载你的应用程序。

在这些情况下，必须在程序集模式下调试。 此外，程序集模式具有调试源中不存在的许多有用的功能。 调试器会自动显示的内存位置的内容和注册访问它们，并显示程序计数器的地址。 此显示使调试一个有价值的工具，可以使用与源调试的程序集。

### <a name="span-iddisassemblycodespanspan-iddisassemblycodespandisassembly-code"></a><span id="disassembly_code"></span><span id="DISASSEMBLY_CODE"></span>反汇编代码

调试器主要分析二进制可执行代码。 而不是以原始格式，在调试器中显示此代码*反汇编*此代码。 也就是说，调试器将代码转换从机器语言为程序集语言。

可以显示生成的代码 (称为*反汇编代码*) 采用多种不同方法：

-   [ **U （反汇编）** ](u--unassemble-.md)命令进行反汇编，并显示机器语言的指定的部分。

-   [ **Uf （反汇编函数）** ](uf--unassemble-function-.md)命令进行反汇编，并显示一个函数。

-   [ **（从物理内存的反汇编） 向上**](up--unassemble-from-physical-memory-.md)命令进行反汇编，并显示已存储在物理内存的机器语言的指定的部分。

-   [ **(反汇编真实模式 BIOS)** ](ur--unassemble-real-mode-bios-.md)命令进行反汇编，并显示指定的 16 位实模式代码。

-   [ **Ux (反汇编 x86 BIOS)** ](ux--unassemble-x86-bios-.md)命令进行反汇编，并显示在指定地址处设置的基于 x86 的 BIOS 代码指令。

-   (仅 WinDbg)[反汇编窗口](view---disassembly.md)进行反汇编，并显示机器语言的指定的部分。 此窗口将自动激活，如果您选择**会自动打开反汇编**命令**窗口**菜单。 此外可以通过单击来打开此窗口**反汇编**上**视图**菜单中，按 alt + 7，或按**反汇编 (alt + 7)** 按钮 (![屏幕截图反汇编按钮的](images/tbdisasm2.png)) WinDbg 工具栏上。

反汇编显示四个列中将显示： 地址偏移量、 二进制代码、 汇编语言助记键和程序集语言的详细信息。 下面的示例演示此显示。

```dbgcmd
0040116b    45          inc         ebp            
0040116c    fc          cld                        
0040116d    8945b0      mov         eax,[ebp-0x1c] 
```

右侧的代表当前程序计数器的线，屏幕将显示的任何内存位置或要访问的寄存器的值。 如果此行包含分支指令，表示法**\[b = 1\]** 或**\[b = 0\]** 出现。 此表示法表示一个分支或未被占用，分别。

可以使用[ **.asm （更改反汇编选项）** ](-asm--change-disassembly-options-.md)命令以更改反汇编的指令的显示方式。

在 WinDbg 的反汇编窗口中，突出显示的行，表示当前的程序计数器。 在其中设置断点的行也会突出显示。

此外可以使用以下命令来操作程序集代码：

-   [  **\# （搜索反汇编模式）** ](---search-for-disassembly-pattern-.md)命令会搜索特定模式的内存区域。 此命令相当于搜索反汇编显示四列。

-   [ **（组装）** ](a--assemble-.md)命令可以获取程序集指令并将它们转换为二进制的机器代码。

### <a name="span-idassemblymodeandsourcemodespanspan-idassemblymodeandsourcemodespanassembly-mode-and-source-mode"></a><span id="assembly_mode_and_source_mode"></span><span id="ASSEMBLY_MODE_AND_SOURCE_MODE"></span>程序集模式和源模式

调试器有两种不同的操作模式：*程序集模式*并*源模式*。

时单步执行通过应用程序后，单步执行的大小是一个程序集代码行或源代码，具体取决于模式的一个行。

多个命令创建不同的数据显示，具体取决于模式。

在 WinDbg 中，[反汇编窗口](disassembly-window.md)或单步执行程序集模式中的应用程序运行时将自动移动到前台。 在源模式[源窗口](source-window.md)将移到前台。

若要设置模式，可以执行下列任一操作：

-   使用[ **l +，l-（设置源选项）** ](l---l---set-source-options-.md)命令来控制模式。 **L-t**命令将激活程序集模式。

-   (仅 WinDbg)清除**源模式**命令**调试**菜单会导致调试器输入程序集模式。此外可以单击**源模式关闭**按钮 (![源模式关闭按钮的屏幕截图](images/tbasm.png)) 工具栏上。

在 WinDbg 中，在程序集模式下，当**ASM**将显示在状态栏上可见。

在 WinDbg 的反汇编窗口中的快捷菜单包含**突出显示当前的源行中的说明**命令。 此命令会突出显示所有对应于当前的源行的说明。 通常情况下，包含一个源行对应于多个程序集指令。 如果代码已经过优化，这些程序集指令可能不是连续的。 **突出显示当前的源行中的说明**命令，您可以找到所有从当前源行组合的说明。

### <a name="span-idassemblylanguagesourcefilesspanspan-idassemblylanguagesourcefilesspanassembly-language-source-files"></a><span id="assembly_language_source_files"></span><span id="ASSEMBLY_LANGUAGE_SOURCE_FILES"></span>程序集语言源文件

如果你的应用程序在程序集语言编写的调试器会生成反汇编可能与原始代码不完全匹配。 具体而言，进行任何操作和提出的意见将不会显示。

如果你想要调试你的代码通过引用原始.asm 文件，则必须使用源模式调试。 您可以加载的程序集文件，如 C 或 c + + 源文件。 有关调试此类的详细信息，请参阅[在源模式中进行调试](debugging-in-source-mode.md)。

 

 





