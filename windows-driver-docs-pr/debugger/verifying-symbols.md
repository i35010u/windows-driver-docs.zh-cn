---
title: 验证符号
description: 验证符号
ms.assetid: 61b4fcce-960b-4091-b575-4dd53c39cff2
keywords:
- 符号验证
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ef6c6bcf0cb03a3924091da76a53914535320a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520266"
---
# <a name="verifying-symbols"></a>验证符号


## <span id="ddk_verifying_symbols_dbg"></span><span id="DDK_VERIFYING_SYMBOLS_DBG"></span>


符号问题可以显示在不同的方式。 可能是堆栈跟踪显示的信息不正确或无法识别的堆栈中函数的名称。 或者可能是调试器命令无法了解模块、 函数、 变量、 结构或数据类型的名称。

如果您怀疑，调试器将不加载符号正确，有几个可用于调查此问题的步骤。

首先，使用[ **lm （列表加载模块）** ](lm--list-loaded-modules-.md)命令以显示已加载模块的符号信息的列表。 以下是此命令的最有用的格式：

```dbgcmd
0:000> lml 
```

如果使用的 WinDbg 中，[调试 |模块](debug---modules.md)菜单命令使你可以查看此信息。

应特别注意的任何注释或可能会看到这些显示中的缩写。 这些解释，请参阅[符号状态缩写](symbol-status-abbreviations.md)。

如果看不到正确的符号文件，首先要做是检查的符号路径：

```dbgcmd
0:000> .sympath
Current Symbol Path is: d:\MyInstallation\i386\symbols\retail
```

如果您的符号路径有误，请修复此错误。 如果使用内核调试器，请确保本地 %WINDIR%不在您的符号路径。

然后重新加载使用的符号[ **.reload （重新加载模块）** ](-reload--reload-module-.md)命令：

```dbgcmd
0:000> .reload ModuleName 
```

如果您的符号路径是正确的则应激活*干扰性模式*以便您可以看到哪些符号文件**dbghelp**正在加载。 然后重新加载您的模块。 请参阅[设置符号选项](symbol-options.md)有关如何激活干扰性模式的信息。

下面是 Microsoft Windows 符号的"嘈杂"重新加载的示例：

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
11: *** WARNING: symbols checksum and timestamp is wrong 0x0036a4ea 0x00361a83 for ntkrnlmp.exe
```

符号处理程序首先查找匹配的模块正在尝试进行加载 （三个和四个行） 的图像。 图像本身并不总是有必要，但如果存在一个不正确，则符号处理程序通常会失败。 这些行显示调试器找到在图像**d:\\MyInstallation\\i386\\ntkrnlmp.exe**，但时间日期戳不匹配。 由于时间日期戳不匹配，将继续搜索。 接下来，在调试器查找.dbg 文件和与加载的图像相匹配的.pdb 文件。 这些是在 6 到 10 行。 第 11 行指示，即使已加载符号，该映像的时间日期戳不匹配 （也就是说，符号是错误）。

如果符号搜索遇到灾难性故障，会看到窗体的一条消息：

```dbgcmd
ImgHlpFindDebugInfo(00000000, module.dll, c:\MyDir;c:\SomeDir, 0823345, 0) failed
```

原因可能是文件系统故障、 网络错误和损坏.dbg 文件等项。

### <a name="span-iddiagnosingsymbolloadingerrorsspanspan-iddiagnosingsymbolloadingerrorsspandiagnosing-symbol-loading-errors"></a><span id="diagnosing_symbol_loading_errors"></span><span id="DIAGNOSING_SYMBOL_LOADING_ERRORS"></span>诊断符号加载错误

在干扰性模式下，调试器可能会打印出错误代码时它不能加载符号文件。 .Dbg 文件的错误代码列示在 winerror.h 中。 .Pdb 错误代码来自另一个源和打印纯英文文本中的最常见的错误。

.Dbg 文件从 winerror.h 一些常见错误代码为：

<span id="0xB"></span><span id="0xb"></span><span id="0XB"></span>0xB  
错误\_错误\_格式

<span id="0x3"></span><span id="0X3"></span>0x3  
错误\_路径\_不\_找到

<span id="0x35"></span><span id="0X35"></span>0x35  
错误\_错误\_NETPATH

很可能不能因网络错误而加载的符号文件。 如果看到错误\_坏\_格式或错误\_错误\_NETPATH 和您要从另一台计算机在网络上加载符号，请尝试将符号文件复制到主计算机并将其路径放在你的符号路径。 然后尝试重新加载符号。

### <a name="span-idverifyingyoursearchpathandsymbolsspanspan-idverifyingyoursearchpathandsymbolsspanverifying-your-search-path-and-symbols"></a><span id="verifying_your_search_path_and_symbols"></span><span id="VERIFYING_YOUR_SEARCH_PATH_AND_SYMBOLS"></span>验证你的搜索路径和符号

让"c:\\MyDir; c:\\SomeDir"表示您的符号路径。 应在其中你查找有关调试信息？

在情况下，已将二进制文件抽取的调试信息，如免费版本的 Windows，可首先阅读.dbg 文件在以下位置：

```dbgcmd
c:\MyDir\symbols\exe\ntoskrnl.dbg
c:\SomeDir\symbols\exe\ntoskrnl.dbg
c:\MyDir\exe\ntoskrnl.dbg
c:\SomeDir\exe\ntoskrnl.dbg
c:\MyDir\ntoskrnl.dbg
c:\SomeDir\ntoskrnl.dbg
current-working-directory\ntoskrnl.dbg
```

接下来，在以下位置的.pdb 文件所示：

```dbgcmd
c:\MyDir\symbols\exe\ntoskrnl.pdb
c:\MyDir\exe\ntoskrnl.pdb
c:\MyDir\ntoskrnl.pdb
c:\SomeDir\symbols\exe\ntoskrnl.pdb
c:\SomeDir\exe\ntoskrnl.pdb
c:\SomeDir\ntoskrnl.pdb
current-working-directory\ntoskrnl.pdb
```

请注意，在.dbg 文件搜索，调试器交错出现搜索 MyDir 和 SomeDir 目录中，但在.pdb 搜索不。

Windows XP 和更高版本的 Windows 不使用任何.dbg 符号文件。 请参阅[符号和符号文件](symbols-and-symbol-files.md)有关详细信息。

### <a name="span-idmismatchedbuildsspanspan-idmismatchedbuildsspanmismatched-builds"></a><span id="mismatched_builds"></span><span id="MISMATCHED_BUILDS"></span>不匹配的生成

在调试经常更新的计算机上的失败最常见的问题之一是从不同版本不匹配的符号。 此问题的三个常见原因是： 指向错误的生成的符号、 使用私人生成的二进制文件，而无需相应的符号，以及在多处理器计算机上使用的单处理器硬件抽象层 (HAL) 和内核符号。 前两个是只需匹配的二进制文件和符号;更正第三个可以通过重命名你 hal\*.dbg 和 hal.dbg 和 ntoskrnl.dbg ntkrnlmp.dbg。

若要了解哪些版本的 Windows 安装在目标计算机上，请使用[ **vertarget （显示目标计算机版本）** ](vertarget--show-target-computer-version-.md)命令：

```dbgcmd
kd> vertarget 
Windows XP Kernel Version 2505 UP Free x86 compatible
Built by: 2505.main.010626-1514
Kernel base = 0x804d0000 PsLoadedModuleList = 0x80548748
Debug session time: Mon Jul 02 14:41:11 2001
System Uptime: 0 days 0:04:53 
```

### <a name="span-idtestingthesymbolsspanspan-idtestingthesymbolsspantesting-the-symbols"></a><span id="testing_the_symbols"></span><span id="TESTING_THE_SYMBOLS"></span>测试符号

测试符号是更加困难。 它涉及验证的调试器上的堆栈跟踪和查看调试输出是否正确。 下面是一个示例，请尝试：

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

**U**命令 unassembles videoprt.sys videoportfindadapter 字符串。 因为常见堆栈命令，如了正确的调试器上的符号**推送**并**mov**显示在堆栈上。 大多数函数开头添加、 sub 或推送操作使用的基指针 (ebp) 或堆栈指针 (esp)。

如果符号不能正常工作，此选项通常很明显。 Glintmp.sys 没有符号在此示例中由于函数未列出旁边**Glintmp**:

```dbgcmd
kd> kb
Loading symbols for 0xf28d0000     videoprt.sys ->   videoprt.sys
Loading symbols for 0xf9cdd000      glintmp.sys ->   glintmp.sys
*** ERROR: Symbols could not be loaded for glintmp.sys
ChildEBP RetAddr  Args to Child
f29bf1b0 8045b5fa 00000001 0000a100 00000030 ntoskrnl!RtlpBreakWithStatusInstruction
f29bf1b0 8044904e 00000001 0000a100 00000030 ntoskrnl!KeUpdateSystemTime+0x13e
f29bf234 f28d1955 f9b7d000 ffafb2dc f9b7d000 ntoskrnl!READ_REGISTER_ULONG+0x6
f29bf248 f9cde411 f9b7d000 f29bf2b0 f9ba0060 VIDEOPRT!VideoPortReadRegisterUlong+0x27
00000002 00000000 00000000 00000000 00000000 glintMP+0x1411 [No function listed.] 
```

错误的生成符号已加载此堆栈跟踪。 请注意如何有任何列出的前两个调用的函数。 此堆栈跟踪如下所示 win32k.sys 绘制矩形的问题：

```dbgcmd
1: kd> 
1: kd> kb                      [Local        9:50 AM]
Loading symbols for 0xf22b0000       agpcpq.sys ->   agpcpq.sys
*** WARNING: symbols checksum is wrong 0x0000735a 0x00000000 for agpcpq.sys
*** ERROR: Symbols could not be loaded for agpcpq.sys
Loading symbols for 0xa0000000       win32k.sys ->   win32k.sys
*** WARNING: symbols checksum is wrong 0x00191a41 0x001995a9 for win32k.sys
ChildEBP RetAddr  Args to Child
be682b18 f22b372b 82707128 f21c1ffc 826a70f8 agpCPQ+0x125b [No function listed.]
be682b4c a0140dd4 826a72f0 e11410a8 a0139605 agpCPQ+0x372b [No function listed.]
be682b80 a00f5646 e1145100 e1cee560 e1cee560 win32k!vPatCpyRect1_6x6+0x20b
00000001 00000000 00000000 00000000 00000000 win32k!RemoteRedrawRectangle+0x32 
```

下面是正确的堆栈跟踪。 AGP440.sys 真的是问题。 显示在堆栈跟踪的第一项通常出现故障。 请注意 win32k.sys 矩形错误将消失：

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

### <a name="span-idusefulcommandsandextensionsspanspan-idusefulcommandsandextensionsspanuseful-commands-and-extensions"></a><span id="useful_commands_and_extensions"></span><span id="USEFUL_COMMANDS_AND_EXTENSIONS"></span>有用的命令和扩展

下面的命令和扩展可能会很有用跟踪符号问题：

<span id="lm__List_Loaded_Modules_"></span><span id="lm__list_loaded_modules_"></span><span id="LM__LIST_LOADED_MODULES_"></span>[**lm （列出已加载的模块）**](lm--list-loaded-modules-.md)  
列出所有模块并在这些模块中提供的所有符号加载状态。

<span id="_dh_image-header-base"></span><span id="_DH_IMAGE-HEADER-BASE"></span>[**！ dh 映像标头基**](-dh.md)  
显示加载的映像开始标头信息*映像标头基*。

<span id=".RELOAD__N"></span>[**.reload /n**](-reload--reload-module-.md)  
重新加载所有内核符号。

<span id=".reload__image-name_"></span><span id=".RELOAD__IMAGE-NAME_"></span>[**.reload \[image-name\]**](-reload--reload-module-.md)  
（CDB 或仅 WinDbg）重新加载符号的图像*映像名称*。 如果没有*映像名称*指定时，重新加载所有映像的符号。 （它是必需的符号路径发生更改后重新加载符号。）

<span id="_sym_noisy"></span><span id="_SYM_NOISY"></span>[**！ 干扰性的符号**](-sym.md)  
开启详细模式进行符号加载。 这可以用于获取有关模块的加载的信息。 请参阅[设置符号选项](symbol-options.md)有关详细信息。

<span id=".sympath__new-symbol-path_"></span><span id=".SYMPATH__NEW-SYMBOL-PATH_"></span>[**.sympath \[new-symbol-path\]**](-sympath--set-symbol-path-.md)  
设置新的符号路径，或显示当前符号路径。 请参阅[符号路径](symbol-path.md)有关详细信息。

如果内核符号是正确的但如果没有收到完整的堆栈，以下命令可能也很有用：

<span id="X___"></span><span id="x___"></span>[**X \*!**](x--examine-symbols-.md)  
这将列出当前具有加载符号的模块。 这是内核符号是正确的情况下很有用。

<span id=".RELOAD__USER"></span>[**.reload /user**](-reload--reload-module-.md)  
这将尝试重新加载用户模式下的所有符号。 执行内核调试，如果一个进程运行时，已加载符号，并会破坏更高版本出现在另一个进程中时，需要此项。 在这种情况下，除非执行此命令将不加载从新的进程的用户模式符号。

<span id="X_wdmaud__start_"></span><span id="x_wdmaud__start_"></span><span id="X_WDMAUD__START_"></span>[**X wdmaud ！\*开始\\***](x--examine-symbols-.md)  
此命令将列出中的符号**wdmaud**模块名称中包含"start"字符串。 这具有的优势在于它会强制重新加载中的所有符号**wdmaud**，但只在其中显示具有"start"。 （这意味着较短的列表，但由于始终使用"开始"，在其中某些符号，将某些负载已发生的验证。）

用于验证符号一个其他有用的技巧 unassembling 代码。 大多数函数开头添加、 sub 或推送操作使用基指针 (**ebp**) 或堆栈指针 (**esp**或**sp**)。 请尝试 unassembling ([**U 函数**](u--unassemble-.md)) 的某些函数 （从偏移量为零） 到堆栈上验证符号。

### <a name="span-idnetworkandportproblemsspanspan-idnetworkandportproblemsspannetwork-and-port-problems"></a><span id="network_and_port_problems"></span><span id="NETWORK_AND_PORT_PROBLEMS"></span>网络和端口问题

符号文件和连接到调试器时，将会出现问题。 下面是需要请记住，如果遇到问题的一些事项：

-   确定调试电缆连接到测试系统的 COM 端口。

-   检查测试系统的 boot.ini 设置。 寻找 **/debug**交换机，并检查波特率和 COM 端口设置。

-   网络问题可能会影响调试的符号文件是通过网络访问。

-   如果它们不分散到正确的目录的符号树.dll 和.sys 文件具有相同名称 （例如 − mga64.sys 和 mga64.dll） 会将调试器相混淆。

-   内核调试程序都不喜欢生成符号文件替换为私有符号文件。 双精度复选符号路径，执行 **.reload * * * 文件名*表现不正常的符号。 [ **！ Dll** ](-dlls.md)命令有时会很有用。

### <a name="span-idquestionsandmisconceptionsspanspan-idquestionsandmisconceptionsspanquestions-and-misconceptions"></a><span id="questions_and_misconceptions"></span><span id="QUESTIONS_AND_MISCONCEPTIONS"></span>疑问和误解

**问：** 我已成功加载符号，但似乎是错误的堆栈。 是调试器中断？

**答：** 不一定。 您的问题最可能的原因是，你准备了错误的符号。 请在此部分可以确定您是否已加载有效符号中所述的步骤执行。 不要假定由于某些功能工作有有效符号。 例如，您很可能能够执行**dd nt ！ ntbuildnumber**或**u nt ！KeInitializeProcess**与错误的符号。 验证正确使用上面所述的过程。

**问：** 调试器将仍适用于错误的符号？

**答：** 是 / 否。 通常您可以侥幸应付严格不匹配的符号。 例如，从以前的 Windows 生成的符号通常会在某些情况下，但没有任何规则时，此操作有效，而它不会。

**问：** 我正在停止内核调试器中，我想要查看我的用户模式进程的符号。 我可以做它？

**答：** 主要。 对于此方案的支持是不佳，因为内核调试程序不会保留足够信息来跟踪每个进程，在模块加载但合理的解决方法。 若要加载用户模式模块的符号，请执行 **.reload-用户**命令。 这将加载当前上下文的用户模式模块。

**问：** 下面的消息是什么意思？

`*** WARNING: symbols checksum and timestamp is wrong 0x0036d6bf 0x0036ab55 for ntkrnlmp.exe`

**答：** 这意味着 ntkrnlmp.exe 你符号是错误。

 

 





