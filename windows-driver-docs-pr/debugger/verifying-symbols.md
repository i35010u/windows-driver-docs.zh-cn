---
title: 验证符号
description: 验证符号
keywords:
- 符号，验证
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1cc7f291ade27537769a6b4d20eb33f6a217f14
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802969"
---
# <a name="verifying-symbols"></a>验证符号


## <span id="ddk_verifying_symbols_dbg"></span><span id="DDK_VERIFYING_SYMBOLS_DBG"></span>


符号问题可以通过多种方式出现。 堆栈跟踪可能会显示不正确的信息，或者无法标识堆栈中函数的名称。 或者可能是调试器命令未能理解模块、函数、变量、结构或数据类型的名称。

如果怀疑调试器未正确加载符号，则可以执行几个步骤来调查此问题。

首先，使用 " [**lm (列出加载的模块")**](lm--list-loaded-modules-.md) 命令显示带有符号信息的已加载模块的列表。 此命令最有用的形式如下：

```dbgcmd
0:000> lml 
```

如果使用的是 WinDbg， [调试 |模块](debug---modules.md) 菜单命令也可用于查看此信息。

请特别注意在这些显示器中可能会看到的任何注释或缩写。 有关这些类的解释，请参阅 [符号状态缩写](symbol-status-abbreviations.md)。

如果看不到正确的符号文件，则首先要检查符号路径：

```dbgcmd
0:000> .sympath
Current Symbol Path is: d:\MyInstallation\i386\symbols\retail
```

如果符号路径错误，请对其进行修复。 如果使用内核调试器，请确保本地% WINDIR% 不在符号路径上。

然后使用重载 [**(重载模块)**](-reload--reload-module-.md) 命令重新加载符号：

```dbgcmd
0:000> .reload ModuleName 
```

如果符号路径正确，应激活 *干扰模式* ，以便可以看到 **dbghelp.dll** 正在加载的符号文件。 然后重新加载模块。 有关如何激活干扰模式的信息，请参阅 [设置符号选项](symbol-options.md) 。

下面是 Microsoft Windows 符号的 "干扰" 重载的示例：

```dbgcmd
kd> !sym noisy
kd> .reload nt
 1: Kernel Version 2081 MP Checked
 2: Kernel base = 0x80400000 PsLoadedModuleList = 0x80506fa0
 3: DBGHELP: FindExecutableImageEx-> Looking for D:\MyInstallation\i386\ntkrnlmp.exe...mismatched timestamp
 4: DBGHELP: No image file available for ntkrnlmp.exe
 5: DBGHELP: FindDebugInfoFileEx-> Looking for
 6: d:\MyInstallation\i386\symbols\retail\symbols\exe\ntkrnlmp.dbg... no file
 7: DBGHELP: FindDebugInfoFileEx-> Looking for
 8: d:\MyInstallation\i386\symbols\retail\symbols\exe\ntkrnlmp.pdb... no file
 9: DBGHELP: FindDebugInfoFileEx-> Looking for d:\MyInstallation\i386\symbols\retail\exe\ntkrnlmp.dbg... OK
10: DBGHELP: LocatePDB-> Looking for d:\MyInstallation\i386\symbols\retail\exe\ntkrnlmp.pdb... OK
11: **_ WARNING: symbols checksum and timestamp is wrong 0x0036a4ea 0x00361a83 for ntkrnlmp.exe
```

符号处理程序首先查找与正在尝试加载的模块匹配的图像 (第三和第四个) 。 图像本身并非总是必需的，但如果存在错误，则符号处理程序通常会失败。 这些行显示调试器在 _ * D： \\ MyInstallation \\ i386ntkrnlmp.exe * * 找到了一个图像 \\ ，但时间日期戳不匹配。 由于时间日期戳不匹配，因此将继续搜索。 接下来，调试器查找一个 dbg 文件和一个与加载的映像匹配的 .pdb 文件。 它们位于第6行到第10行。 第11行指示即使已加载符号，图像的时间日期戳也不匹配 (也就是说，符号) 错误。

如果符号搜索遇到灾难性故障，则会看到一条形式的消息：

```dbgcmd
ImgHlpFindDebugInfo(00000000, module.dll, c:\MyDir;c:\SomeDir, 0823345, 0) failed
```

这可能是由于文件系统故障、网络错误和 dbg 文件等项导致的。

### <a name="span-iddiagnosing_symbol_loading_errorsspanspan-iddiagnosing_symbol_loading_errorsspandiagnosing-symbol-loading-errors"></a><span id="diagnosing_symbol_loading_errors"></span><span id="DIAGNOSING_SYMBOL_LOADING_ERRORS"></span>诊断符号加载错误

当处于干扰模式下时，调试程序可以在无法加载符号文件时输出错误代码。 Winerror.h 中列出了 dbg 文件的错误代码。 .Pdb 错误代码来自其他源，最常见的错误以纯英文文本打印。

Winerror.h 中的 dbg 文件的一些常见错误代码为：

<span id="0xB"></span><span id="0xb"></span><span id="0XB"></span>0xB  
错误 \_ \_ 格式错误

<span id="0x3"></span><span id="0X3"></span>0x3  
\_ \_ 找不到错误路径 \_

<span id="0x35"></span><span id="0X35"></span>0x35  
错误 \_ \_ NETPATH 错误

由于网络错误，可能无法加载符号文件。 如果出现错误 "错误" \_ \_ 或 \_ "错误 \_ NETPATH 错误"，并且正在从网络上的另一台计算机加载符号，请尝试将符号文件复制到您的主计算机，并将其路径放在您的符号路径中。 然后尝试重新加载符号。

### <a name="span-idverifying_your_search_path_and_symbolsspanspan-idverifying_your_search_path_and_symbolsspanverifying-your-search-path-and-symbols"></a><span id="verifying_your_search_path_and_symbols"></span><span id="VERIFYING_YOUR_SEARCH_PATH_AND_SYMBOLS"></span>验证搜索路径和符号

让 "c： \\ MyDir; c： \\ SomeDir" 表示你的符号路径。 在哪里可以找到调试信息？

在清除了二进制文件（如 Windows 的免费版本）的情况下，首先在以下位置查找一个 dbg 文件：

```dbgcmd
c:\MyDir\symbols\exe\ntoskrnl.dbg
c:\SomeDir\symbols\exe\ntoskrnl.dbg
c:\MyDir\exe\ntoskrnl.dbg
c:\SomeDir\exe\ntoskrnl.dbg
c:\MyDir\ntoskrnl.dbg
c:\SomeDir\ntoskrnl.dbg
current-working-directory\ntoskrnl.dbg
```

接下来，请在以下位置查找 .pdb 文件：

```dbgcmd
c:\MyDir\symbols\exe\ntoskrnl.pdb
c:\MyDir\exe\ntoskrnl.pdb
c:\MyDir\ntoskrnl.pdb
c:\SomeDir\symbols\exe\ntoskrnl.pdb
c:\SomeDir\exe\ntoskrnl.pdb
c:\SomeDir\ntoskrnl.pdb
current-working-directory\ntoskrnl.pdb
```

请注意，在搜索 dbg 文件时，调试器交错搜索 MyDir 和 SomeDir 目录，但在 .pdb 中搜索不到。

Windows XP 和更高版本的 Windows 不使用任何 dbg 符号文件。 有关详细信息，请参阅 [符号和符号文件](symbols-and-symbol-files.md) 。

### <a name="span-idmismatched_buildsspanspan-idmismatched_buildsspanmismatched-builds"></a><span id="mismatched_builds"></span><span id="MISMATCHED_BUILDS"></span>不匹配的生成

经常更新的计算机上调试失败的一个最常见问题是不同生成中的符号不匹配。 此问题的三个常见原因是：使用私下构建的二进制文件而不包含相应的符号来指向错误的生成，并使用单处理器硬件抽象级别 (HAL) 和多处理器计算机上的内核符号。 前两个只是匹配您的二进制文件和符号的问题;第三个可以通过将你的 \* ntkrnlmp 和 ntoskrnl.exe 重命名为 hal 和来更正。

若要了解目标计算机上安装的 Windows 的版本，请使用 [**vertarget (显示目标计算机版本)**](vertarget--show-target-computer-version-.md) 命令：

```dbgcmd
kd> vertarget 
Windows XP Kernel Version 2505 UP Free x86 compatible
Built by: 2505.main.010626-1514
Kernel base = 0x804d0000 PsLoadedModuleList = 0x80548748
Debug session time: Mon Jul 02 14:41:11 2001
System Uptime: 0 days 0:04:53 
```

### <a name="span-idtesting_the_symbolsspanspan-idtesting_the_symbolsspantesting-the-symbols"></a><span id="testing_the_symbols"></span><span id="TESTING_THE_SYMBOLS"></span>测试符号

测试符号会比较困难。 它涉及在调试器上验证堆栈跟踪，并查看调试输出是否正确。 下面是一个尝试示例：

```dbgcmd
kd> u videoprt!videoportfindadapter2
Loading symbols for 0xf2860000     videoprt.sys ->   videoprt.sys

VIDEOPRT!VideoPortFindAdapter2:
f2856f42 55               push    ebp
f2856f43 8bec             mov     ebp,esp
f2856f45 81ecb8010000     sub     esp,0x1b8
f2856f4b 8b4518           mov     eax,[ebp+0x18]
f2856f4e 53               push    ebx
f2856f4f 8365f400         and     dword ptr [ebp-0xc],0x
f2856f53 8065ff00         and     byte ptr [ebp-0x1],0x0
f2856f57 56               push    esi
```

**U** 命令在 videoprt.sys 中 unassembles videoportfindadapter 字符串。 这些符号在调试器中是正确的，因为在堆栈上显示诸如 **推送** 和 **mov** 等常见堆栈命令。 大多数函数都以添加、子或推送操作开始，使用基指针 (ebp) 或堆栈指针 (esp) 。

通常，当符号不能正常工作时很明显。 在此示例中 Glintmp.sys 没有符号，因为未在 **Glintmp** 旁边列出函数：

```dbgcmd
kd> kb
Loading symbols for 0xf28d0000     videoprt.sys ->   videoprt.sys
Loading symbols for 0xf9cdd000      glintmp.sys ->   glintmp.sys
**_ ERROR: Symbols could not be loaded for glintmp.sys
ChildEBP RetAddr  Args to Child
f29bf1b0 8045b5fa 00000001 0000a100 00000030 ntoskrnl!RtlpBreakWithStatusInstruction
f29bf1b0 8044904e 00000001 0000a100 00000030 ntoskrnl!KeUpdateSystemTime+0x13e
f29bf234 f28d1955 f9b7d000 ffafb2dc f9b7d000 ntoskrnl!READ_REGISTER_ULONG+0x6
f29bf248 f9cde411 f9b7d000 f29bf2b0 f9ba0060 VIDEOPRT!VideoPortReadRegisterUlong+0x27
00000002 00000000 00000000 00000000 00000000 glintMP+0x1411 [No function listed.] 
```

为此堆栈跟踪加载了错误的生成符号。 请注意，前两个调用没有列出任何函数。 此堆栈跟踪类似于 win32k.sys 绘制矩形的问题：

```dbgcmd
1: kd> 
1: kd> kb                      [Local        9:50 AM]
Loading symbols for 0xf22b0000       agpcpq.sys ->   agpcpq.sys
_*_ WARNING: symbols checksum is wrong 0x0000735a 0x00000000 for agpcpq.sys
_*_ ERROR: Symbols could not be loaded for agpcpq.sys
Loading symbols for 0xa0000000       win32k.sys ->   win32k.sys
_*_ WARNING: symbols checksum is wrong 0x00191a41 0x001995a9 for win32k.sys
ChildEBP RetAddr  Args to Child
be682b18 f22b372b 82707128 f21c1ffc 826a70f8 agpCPQ+0x125b [No function listed.]
be682b4c a0140dd4 826a72f0 e11410a8 a0139605 agpCPQ+0x372b [No function listed.]
be682b80 a00f5646 e1145100 e1cee560 e1cee560 win32k!vPatCpyRect1_6x6+0x20b
00000001 00000000 00000000 00000000 00000000 win32k!RemoteRedrawRectangle+0x32 
```

下面是正确的堆栈跟踪。 问题确实与 AGP440.sys 有关。 堆栈跟踪上出现的第一项通常为错误。 请注意，win32k.sys 矩形错误已消失：

```dbgcmd
1: kd> kb                      [Local        9:49 AM]
ChildEBP RetAddr  Args to Child
be682b18 f22b372b 82707128 f21c1ffc 826a70f8 agpCPQ!AgpReleaseMemory+0x88
be682b30 f20a385c 82703638 e183ec68 00000000 agpCPQ!AgpInterfaceReleaseMemory+0x8b
be682b4c a0140dd4 826a72f0 e11410a8 a0139605 VIDEOPRT!AgpReleasePhysical+0x44
be682b58 a0139605 e1cee560 e11410a8 a00e5f0a win32k!OsAGPFree+0x14
be682b64 a00e5f0a e1cee560 e11410a8 e1cee560 win32k!AGPFree+0xd
be682b80 a00f5646 e1145100 e1cee560 e1cee560 win32k!HeapVidMemFini+0x49
be682b9c a00f5c20 e1cee008 e1cee008 be682c0c win32k!vDdDisableDriver+0x3a
be682bac a00da510 e1cee008 00000000 be682c0c win32k!vDdDisableDirectDraw+0x2d
be682bc4 a00da787 00000000 e1843df8 e1843de8 win32k!PDEVOBJ__vDisableSurface+0x27
be682bec a00d59fb 00000000 e1843de8 00000000 win32k!PDEVOBJ__vUnreferencePdev+0x204
be682c04 a00d7421 e1cee008 82566a98 00000001 win32k!DrvDestroyMDEV+0x30
be682ce0 a00a9e7f e1843e10 e184a008 00000000 win32k!DrvChangeDisplaySettings+0x8b3
be682d20 a008b543 00000000 00000000 00000000 win32k!xxxUserChangeDisplaySettings+0x106
be682d48 8045d119 00000000 00000000 00000000 win32k!NtUserChangeDisplaySettings+0x48
be682d48 77e63660 00000000 00000000 00000000 ntkrnlmp!KiSystemService+0xc9 
```

### <a name="span-iduseful_commands_and_extensionsspanspan-iduseful_commands_and_extensionsspanuseful-commands-and-extensions"></a><span id="useful_commands_and_extensions"></span><span id="USEFUL_COMMANDS_AND_EXTENSIONS"></span>有用的命令和扩展

以下命令和扩展可用于跟踪符号问题：

<span id="lm__List_Loaded_Modules_"></span><span id="lm__list_loaded_modules_"></span><span id="LM__LIST_LOADED_MODULES_"></span>[_ *lm (列出加载的模块)**](lm--list-loaded-modules-.md)  
列出所有模块，并提供这些模块中所有符号的加载状态。

<span id="_dh_image-header-base"></span><span id="_DH_IMAGE-HEADER-BASE"></span>[**！ dh 映像-标头-基本**](-dh.md)  
显示加载的映像的标头信息（从 *图像标头开始）*。

<span id=".RELOAD__N"></span>[**。重装/n**](-reload--reload-module-.md)  
重新加载所有内核符号。

<span id=".reload__image-name_"></span><span id=".RELOAD__IMAGE-NAME_"></span>[**。重新加载 \[ 映像名称\]**](-reload--reload-module-.md)  
 (CDB 或 WinDbg 仅) 为映像 *映像名称* 加载符号。 如果未指定 *映像名称* ，则为所有映像重新加载符号。  (在符号路径更改后必须重新加载符号。 ) 

<span id="_sym_noisy"></span><span id="_SYM_NOISY"></span>[**！符号干扰**](-sym.md)  
打开符号加载的详细模式。 这可用于获取有关模块加载的信息。 有关详细信息，请参阅 [设置符号选项](symbol-options.md) 。

<span id=".sympath__new-symbol-path_"></span><span id=".SYMPATH__NEW-SYMBOL-PATH_"></span>[**. sympath \[\]**](-sympath--set-symbol-path-.md)  
设置新的符号路径，或显示当前的符号路径。 有关详细信息，请参阅 [符号路径](symbol-path.md) 。

如果内核符号正确，但没有获取完整的堆栈，以下命令也可能会很有用：

<span id="X___"></span><span id="x___"></span>[**X \* ！**](x--examine-symbols-.md)  
这将列出当前已加载符号的模块。 如果内核符号正确，则此方法很有用。

<span id=".RELOAD__USER"></span>[**。重新加载/user**](-reload--reload-module-.md)  
这将尝试重新加载所有用户模式符号。 如果在一个进程正在运行时加载了符号，并在另一个进程中发生了中断，则在执行内核调试时需要执行此操作。 在这种情况下，将不会加载新进程中的用户模式符号，除非执行此命令。

<span id="X_wdmaud__start_"></span><span id="x_wdmaud__start_"></span><span id="X_WDMAUD__START_"></span>[**X wdmaud！ \*start\\***](x--examine-symbols-.md)  
这将仅列出名称中包含 "start" 字符串的 **wdmaud** 模块中的符号。 这种方法的优点在于，它会强制重新加载 **wdmaud** 中的所有符号，但只会在其中显示具有 "start" 的符号。  (这意味着较短的列表，但由于其中始终有一些符号为 "start" 的符号，因此会对负载进行一些验证。 ) 

验证符号的另一种有用方法是 unassembling 代码。 大多数函数都以添加、子或推送操作开始，使用基指针 (**ebp**) 或堆栈指针 (**esp** 或 **sp**) 。 尝试 unassembling ([**U 函数**](u--unassemble-.md)) 堆栈上的某些函数 (从偏移零) 来验证符号。

### <a name="span-idnetwork_and_port_problemsspanspan-idnetwork_and_port_problemsspannetwork-and-port-problems"></a><span id="network_and_port_problems"></span><span id="NETWORK_AND_PORT_PROBLEMS"></span>网络和端口问题

当符号文件和连接到调试器时，将出现问题。 如果遇到问题，请记住以下几点：

-   确定测试系统上调试电缆连接到的 COM 端口。

-   检查测试系统的 boot.ini 设置。 查找 **/debug** 开关并检查波特率和 COM 端口设置。

-   如果通过网络访问符号文件，则网络问题可能会干扰调试。

-   如果 .dll 和 .sys 文件具有相同的名称 (例如− mga64.sys 并且 mga64.dll) 会使调试器混淆，前提是它们没有分隔到符号树的正确目录中。

-   内核调试器并不总是像将生成符号文件替换为私有符号文件。 请仔细检查符号路径，然后执行 **. 重载** 符号上的 reload.sql _文件名_。 [**！ Dll**](-dlls.md)命令有时很有用。

### <a name="span-idquestions_and_misconceptionsspanspan-idquestions_and_misconceptionsspanquestions-and-misconceptions"></a><span id="questions_and_misconceptions"></span><span id="QUESTIONS_AND_MISCONCEPTIONS"></span>问题和误解

**问：** 我已成功加载符号，但堆栈似乎错误。 调试器是否中断？

**答：** 不一定。 您的问题最可能的原因是您的符号不正确。 完成本部分中概述的步骤，确定是否已加载有效符号。 不要这样做，因为某些东西会使用有效符号。 例如，你很有可能能够执行 **dd nt！ ntbuildnumber** 或 **u nt！** 带有错误符号的 KeInitializeProcess。 使用上述过程验证它们是否正确。

**问：** 调试器是否仍然使用错误的符号？

**答：** 是和否。 通常，您可以摆脱不严格匹配的符号。 例如，在某些情况下，以前的 Windows 版本中的符号通常会起作用，但没有适用于这种情况的规则。

**问：** 我在内核调试器中已停止，我想要查看用户模式进程的符号。 是否可以执行此操作？

**答：** 主要. 对此方案的支持很糟糕，因为内核调试器并不保留足够的信息来跟踪每个进程的模块负载，而是合理的解决方法。 若要为用户模式模块加载符号，请执行 **reload.sql-user** 命令。 这会加载当前上下文的用户模式模块。

**问：** 以下消息是什么意思？

`**_ WARNING: symbols checksum and timestamp is wrong 0x0036d6bf 0x0036ab55 for ntkrnlmp.exe`

_ *A：** 表示 ntkrnlmp.exe 的符号不正确。

 

 





