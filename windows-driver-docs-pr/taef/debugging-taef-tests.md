---
title: 调试 TAEF 测试
description: 调试 TAEF 测试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 763f3d3112544196c939d769050a1352f20ad295
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840469"
---
# <a name="debugging-taef-tests"></a>调试 TAEF 测试


## <a name="span-iddebugger_configurationspanspan-iddebugger_configurationspanspan-iddebugger_configurationspandebugger-configuration"></a><span id="Debugger_configuration"></span><span id="debugger_configuration"></span><span id="DEBUGGER_CONFIGURATION"></span>调试器配置


默认情况下，测试用例在单独的进程中执行，而不是 TE.exe： TE.ProcessHost.exe。

## <a name="span-iddebugging_child_processes_of_teexe__windbg_cdb_only_spanspan-iddebugging_child_processes_of_teexe__windbg_cdb_only_spandebugging-child-processes-of-teexe-windbgcdb-only"></a><span id="debugging_child_processes_of_te.exe__windbg_cdb_only_"></span><span id="DEBUGGING_CHILD_PROCESSES_OF_TE.EXE__WINDBG_CDB_ONLY_"></span>仅 (windbg/cdb TE.exe 调试子进程) 


如果使用 cdb 或 windbg 等调试器，只需将 "-o" 开关传递到调试器。 这会将调试器配置为自动调试子进程，所有 withinin 相同的调试器实例。

例如：

``` syntax
windbg -o te.exe MyTests.dll
```

然后，若要切换到运行测试的进程，请使用 | (pipe) 命令。 用于切换进程的管道命令 exaclty 用作用于切换线程的 ~ (tilda) 命令。

例如：

``` syntax
|1s - sets the current process to the second loaded process.
```

## <a name="span-idrunning_tests__inproc___visual_studio_windbg_cdb_spanspan-idrunning_tests__inproc___visual_studio_windbg_cdb_spanspan-idrunning_tests__inproc___visual_studio_windbg_cdb_spanrunning-tests-inproc-visual-studiowindbgcdb"></a><span id="Running_Tests__InProc___Visual_Studio_windbg_cdb_"></span><span id="running_tests__inproc___visual_studio_windbg_cdb_"></span><span id="RUNNING_TESTS__INPROC___VISUAL_STUDIO_WINDBG_CDB_"></span>运行测试 "InProc" (Visual Studio/windbg/cdb) 


如果你更愿意使用 Visual Studio 进行调试，则上述方法将不适合你。 在这种情况下，只需将调试器配置为运行 TE.exe，在中为测试用例设置相应的断点，然后将/inproc 开关传递到 TE.exe。 这将确保所有测试都在 TE.exe 进程内运行，而不是生成新的进程。

例如：

``` syntax
start devenv /debugexe te.exe MyTests.dll /inproc
```

上面的命令将启动 Visual Studio。 接下来，打开测试用例的源代码，并设置相应的断点。 最后，按 F5 以启动测试用例，并且应在第一个断点处中断 (如果已正确加载了符号) 。

上面所述的步骤仅适用于在 Visual Studio 中设置的正确符号。 至少需要将符号设置为要调试的测试 dll。 若要在 Visual Studio 中设置符号：

-   选择工具菜单
-   选择选项 .。。
-   选择左侧树状菜单上的 "调试"
-   选择要调试的符号
-   在 "符号文件 (\* .pdb) location：" 部分下输入符号路径
-   保存设置

## <a name="span-idautomatically_breaking_into_the_debugger___breakoncreate__and__breakoninvoke__spanspan-idautomatically_breaking_into_the_debugger___breakoncreate__and__breakoninvoke__spanspan-idautomatically_breaking_into_the_debugger___breakoncreate__and__breakoninvoke__spanautomatically-breaking-into-the-debugger-breakoncreate-and-breakoninvoke"></a><span id="Automatically_Breaking_into_the_Debugger___breakOnCreate__and__breakOnInvoke__"></span><span id="automatically_breaking_into_the_debugger___breakoncreate__and__breakoninvoke__"></span><span id="AUTOMATICALLY_BREAKING_INTO_THE_DEBUGGER___BREAKONCREATE__AND__BREAKONINVOKE__"></span>自动中断到调试器 ( "breakOnCreate" 和 "breakOnInvoke" ) 


为了简化调试过程，Taef 提供了在每个测试类实例化之前自动中断到调试器的功能，并在调用每个测试方法之前自动中断。

例如：

``` syntax
cdb -gG te.exe MyTests.dll /inproc /breakOnCreate /breakOnInvoke
```

上面的命令将在 cdb 下启动 Te.exe。 在实例化每个测试类之前和调用每个测试方法之前，Taef 将中断到调试器。

**注意：** 建议在调试器下运行 Te.exe 时使用此功能，同时指定/inProc 选项。

 

 





