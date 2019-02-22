---
title: 使用 DBH
description: 使用 DBH
ms.assetid: c544013d-e925-40bf-b76d-bf9cefb9fd6d
keywords:
- DBH，使用
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b11826f966fc73ef4f0404c93ab0f5f00e88027
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544114"
---
# <a name="using-dbh"></a>使用 DBH


DBH 是一个命令行工具，提供了许多 DbgHelp API (dbghelp.dll) 中的函数。 它可以显示的符号文件的内容的信息、 在文件中，显示的符号的具体详细信息和搜索的各种条件匹配的符号文件。

DBH 提供的功能是类似于如提供在 WinDbg、 KD 和 CDB 命令[ **（检查符号） x**](x--examine-symbols-.md)。

### <a name="span-idrunningdbhininteractivemodespanspan-idrunningdbhininteractivemodespanrunning-dbh-in-interactive-mode"></a><span id="running_dbh_in_interactive_mode"></span><span id="RUNNING_DBH_IN_INTERACTIVE_MODE"></span>在交互模式下运行 DBH

在其中指定你想要调查的符号的目标模块的简单命令行启动 DBH。 目标模块可以是 EXE 程序或 PDB 符号文件。 此外可以指定的进程 ID (PID) 来调查。 请参阅[ **DBH 命令行选项**](dbh-command-line-options.md)有关完整语法。

DBH 启动时，它加载指定模块的符号，然后向你呈现可以在其中键入命令的各种提示。 请参阅[DBH 命令](dbh-commands.md)有关可用命令的列表。

例如，按以下顺序通过与进程 ID 4672 指定目标进程来启动 DBH 然后执行**枚举**DBH 提示符的命令，以显示符号匹配特定模式，然后执行**q**命令退出 DBH:

```console
C:\> dbh -p:4672 
            400000 : TimeTest
          77820000 : ntdll
          77740000 : kernel32

pid:4672 mod:TimeTest[400000]: enum TimeTest!ma* 

 index            address     name
     1             42cc56 :   main
     3             415810 :   malloc
     5             415450 :   mainCRTStartup

pid:4672 mod:TimeTest[400000]: q 

goodbye 
```

### <a name="span-idrunningdbhinbatchmodespanspan-idrunningdbhinbatchmodespanrunning-dbh-in-batch-mode"></a><span id="running_dbh_in_batch_mode"></span><span id="RUNNING_DBH_IN_BATCH_MODE"></span>在批处理模式下运行 DBH

如果你想要运行只能有一个 DBH 命令，可以指定其命令行的末尾。 这将导致 DBH 启动、 加载指定的模块、 运行指定的命令，并随后退出。

例如，可以使用单个命令行替换为前面的示例：

```console
C:\> dbh -p:4672 enum TimeTest!ma* 
           400000 : TimeTest
         77820000 : ntdll
         77740000 : kernel32

index            address     name
    1             42cc56 :   main
    3             415810 :   malloc
    5             415450 :   mainCRTStartup 
```

调用此方法的运行 DBH*批处理模式下*，因为它可以轻松地使用在批处理文件中。 此版本的命令行还可以跟一个管道 ( **|** ) 这 DBH 输出重定向到另一个程序。

### <a name="span-idspecifyingthetargetspanspan-idspecifyingthetargetspanspecifying-the-target"></a><span id="specifying_the_target"></span><span id="SPECIFYING_THE_TARGET"></span>指定目标

DBH 可以选择一个目标以三种方式： 通过正在运行的进程的进程 ID、 可执行文件的名称或符号文件的名称。 例如，如果只有一个实例当前正在运行，与进程 ID 为 1234，MyProg.exe 然后以下命令是几乎等效的：

```console
C:\> dbh -v -p:1234 
C:\> dbh -v c:\mydir\myprog.exe 
C:\> dbh -v c:\mydir\myprog.pdb 
```

这些命令之间的区别在于，当您通过指定的进程 ID 启动 DBH，DBH 使用此进程正在使用的实际虚拟地址。 当您通过指定可执行文件的名称或符号文件名称启动 DBH 时，DBH 假定模块的基址为标准值 (例如，0x01000000)。 然后，可以使用**基**命令指定实际的基址，因此转换模块中的所有符号的地址。

DBH 未附加到目标进程中调试程序的方式处理。 DBH 不会导致一个进程来开始或结束，也可以更改该进程的运行方式。 对于 DBH 附加到进程按进程 ID，目标进程必须处于运行状态，但一旦启动 DBH 可以终止目标进程和 DBH 能否继续访问其符号。

### <a name="span-iddecoratedandundecoratedsymbolsspanspan-iddecoratedandundecoratedsymbolsspandecorated-and-undecorated-symbols"></a><span id="decorated_and_undecorated_symbols"></span><span id="DECORATED_AND_UNDECORATED_SYMBOLS"></span>修饰和未修饰的符号

默认情况下，DBH 使用未修饰的符号名称时显示和搜索符号。 如果您关闭[SYMOPT\_UNDNAME](symbol-options.md#symopt-undname)符号选项，或者包括 DBH 命令行中的-d 选项，将包含修饰。

符号修饰的信息，请参阅[公共和私有符号](public-and-private-symbols.md)。

### <a name="span-idexitingdbhspanspan-idexitingdbhspanexiting-dbh"></a><span id="exiting_dbh"></span><span id="EXITING_DBH"></span>退出 DBH

若要退出 DBH，请使用**q** DBH 提示符命令。

 

 





