---
title: 调试 TAEF 测试
description: 调试 TAEF 测试
ms.assetid: 0239547F-EF29-45e0-BACF-ED0F6C07DB99
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16a0ee06c32bdc2d28ccc8f4186e8b8181bff24c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391371"
---
# <a name="debugging-taef-tests"></a>调试 TAEF 测试


## <a name="span-iddebuggerconfigurationspanspan-iddebuggerconfigurationspanspan-iddebuggerconfigurationspandebugger-configuration"></a><span id="Debugger_configuration"></span><span id="debugger_configuration"></span><span id="DEBUGGER_CONFIGURATION"></span>调试器配置


默认情况下，于 TE.exe 的单独进程中执行测试用例：TE.ProcessHost.exe.

## <a name="span-iddebuggingchildprocessesofteexewindbgcdbonlyspanspan-iddebuggingchildprocessesofteexewindbgcdbonlyspandebugging-child-processes-of-teexe-windbgcdb-only"></a><span id="debugging_child_processes_of_te.exe__windbg_cdb_only_"></span><span id="DEBUGGING_CHILD_PROCESSES_OF_TE.EXE__WINDBG_CDB_ONLY_"></span>调试子进程的 TE.exe (仅 windbg/cdb)


如果使用如 cdb 或 windbg 调试器，可以只是传递-o 切换到调试器。 这会配置调试器以自动调试子进程，所有 withinin 同一个调试器实例。

例如：

``` syntax
windbg -o te.exe MyTests.dll
```

然后切换到运行测试的过程，使用 |（管道） 命令。 切换进程的管道命令是使用的 exaclty 为 ~ (tilda) 命令用于切换的线程。

例如：

``` syntax
|1s - sets the current process to the second loaded process.
```

## <a name="span-idrunningtestsinprocvisualstudiowindbgcdbspanspan-idrunningtestsinprocvisualstudiowindbgcdbspanspan-idrunningtestsinprocvisualstudiowindbgcdbspanrunning-tests-inproc-visual-studiowindbgcdb"></a><span id="Running_Tests__InProc___Visual_Studio_windbg_cdb_"></span><span id="running_tests__inproc___visual_studio_windbg_cdb_"></span><span id="RUNNING_TESTS__INPROC___VISUAL_STUDIO_WINDBG_CDB_"></span>运行测试"InProc"(Visual Studio/windbg/cdb)


如果想要使用 Visual Studio 进行调试，上面的方法不会为您。 在这种情况下，只需要配置你调试器运行 TE.exe、 设置测试用例中的相应断点并传递到 TE.exe /inproc 开关。 这将确保在 TE.exe 内运行所有测试，而不是生成新的进程的进程。

例如：

``` syntax
start devenv /debugexe te.exe MyTests.dll /inproc
```

上面的命令将启动 Visual Studio。 接下来打开测试用例的源代码并设置适当的断点。 最后，按的 F5 以启动测试用例以及它应中断对第一个断点 （如果已正确加载符号）。

上面所述的步骤仅使用 Visual Studio 中设置正确的符号。 至少，您需要将符号设置为正在调试的测试 dll。 若要在 Visual Studio 中设置符号：

-   选择工具菜单
-   选择选项...
-   选择调试在左侧树中查找菜单
-   在调试下选择符号
-   输入下符号文件的符号路径 (\*.pdb) 位置： 部分
-   保存设置

## <a name="span-idautomaticallybreakingintothedebuggerbreakoncreateandbreakoninvokespanspan-idautomaticallybreakingintothedebuggerbreakoncreateandbreakoninvokespanspan-idautomaticallybreakingintothedebuggerbreakoncreateandbreakoninvokespanautomatically-breaking-into-the-debugger-breakoncreate-and-breakoninvoke"></a><span id="Automatically_Breaking_into_the_Debugger___breakOnCreate__and__breakOnInvoke__"></span><span id="automatically_breaking_into_the_debugger___breakoncreate__and__breakoninvoke__"></span><span id="AUTOMATICALLY_BREAKING_INTO_THE_DEBUGGER___BREAKONCREATE__AND__BREAKONINVOKE__"></span>自动中断到调试器 （"breakOnCreate"和"breakOnInvoke"）


为了简化调试过程，Taef 提供了实例化每个测试类和/或每个测试方法调用之前自动进入调试器的功能。

例如：

``` syntax
cdb -gG te.exe MyTests.dll /inproc /breakOnCreate /breakOnInvoke
```

上面的命令将启动下 cdb Te.exe。 Taef 将中断到调试器正确实例化每个测试类时，并在每个测试之前调用方法之前。

**注意：** 建议您在调试器中，以及后缀 /inProc 选项运行 Te.exe 时使用此功能。

 

 





