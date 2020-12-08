---
title: 使用 DBH
description: 使用 DBH
keywords:
- THIS->DBH，使用
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73801a230c2301a542dd04b73f0b8b02e24b7a65
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803156"
---
# <a name="using-dbh"></a>使用 DBH


THIS->DBH 是一个命令行工具，可在 Dbghelp.dll API ( # A0) 中公开许多功能。 它可以显示有关符号文件内容的信息，在文件中显示符号的特定详细信息，并在文件中搜索匹配各种条件的符号。

THIS->DBH 提供的功能类似于在 WinDbg、KD 和 CDB 中提供的功能，例如 [**x (检查符号)**](x--examine-symbols-.md)。

### <a name="span-idrunning_dbh_in_interactive_modespanspan-idrunning_dbh_in_interactive_modespanrunning-dbh-in-interactive-mode"></a><span id="running_dbh_in_interactive_mode"></span><span id="RUNNING_DBH_IN_INTERACTIVE_MODE"></span>在交互模式下运行 THIS->DBH

使用简单的命令行启动 THIS->DBH，在该命令行中指定要调查其符号的目标模块。 目标模块可以是 EXE 程序或 PDB 符号文件。 你还可以指定要调查 (PID) 的进程 ID。 有关完整的语法，请参阅 [**this->dbh Command-Line 选项**](dbh-command-line-options.md) 。

当 THIS->DBH 启动时，它会为指定的模块加载符号，并向您提供一个提示，你可以在其中键入各种命令。 有关可用命令的列表，请参阅 [This->dbh 命令](dbh-commands.md) 。

例如，以下序列通过指定进程 ID 为4672的目标进程来启动 THIS->DBH，然后在 THIS->DBH 提示符下执行 **enum** 命令，以显示与特定模式匹配的符号，然后执行 **q** 命令以退出 this->dbh：

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

### <a name="span-idrunning_dbh_in_batch_modespanspan-idrunning_dbh_in_batch_modespanrunning-dbh-in-batch-mode"></a><span id="running_dbh_in_batch_mode"></span><span id="RUNNING_DBH_IN_BATCH_MODE"></span>在批处理模式下运行 THIS->DBH

如果只想运行单个 THIS->DBH 命令，可以在命令行的末尾指定它。 这将导致 THIS->DBH 启动、加载指定的模块，运行指定的命令，然后退出。

例如，可以使用单个命令行替换前面的示例：

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

此运行 THIS->DBH 的方法称为 *批处理模式*，因为它可在批处理文件中轻松使用。 此版本的命令行之后还可以后跟一个管道 ( **|** ) 将 this->dbh 输出重定向到另一个程序。

### <a name="span-idspecifying_the_targetspanspan-idspecifying_the_targetspanspecifying-the-target"></a><span id="specifying_the_target"></span><span id="SPECIFYING_THE_TARGET"></span>指定目标

THIS->DBH 可以通过以下三种方式选择目标：按正在运行的进程的进程 ID、可执行文件的名称或符号文件的名称。 例如，如果只有一个当前正在运行的 MyProg.exe 实例，并且进程 ID 为1234，则以下命令几乎等效：

```console
C:\> dbh -v -p:1234 
C:\> dbh -v c:\mydir\myprog.exe 
C:\> dbh -v c:\mydir\myprog.pdb 
```

这些命令的一个区别是，当你通过指定进程 ID 启动 THIS->DBH 时，THIS->DBH 将使用此进程使用的实际虚拟地址。 通过指定可执行文件名称或符号文件名启动 THIS->DBH 时，THIS->DBH 假设模块的基址为标准值 (例如，0x01000000) 。 然后，可以使用 **基本** 命令来指定实际的基址，从而改变模块中所有符号的地址。

THIS->DBH 不会以调试器执行的方式附加到目标进程。 THIS->DBH 不会导致进程开始或结束，也不能更改进程的运行方式。 对于 THIS->DBH 通过其进程 ID 附加到进程，目标进程必须正在运行，但一旦启动了 THIS->DBH，就可以终止目标进程，THIS->DBH 将继续访问其符号。

### <a name="span-iddecorated_and_undecorated_symbolsspanspan-iddecorated_and_undecorated_symbolsspandecorated-and-undecorated-symbols"></a><span id="decorated_and_undecorated_symbols"></span><span id="DECORATED_AND_UNDECORATED_SYMBOLS"></span>修饰和未修饰符号

默认情况下，在显示和搜索符号时，THIS->DBH 使用未修饰符号名称。 如果关闭 [SYMOPT \_ UNDNAME](symbol-options.md#symopt-undname) symbol 选项，或在 this->dbh 命令行中包括-d 选项，则会包含修饰。

有关符号修饰的信息，请参阅 [公共和私有符号](public-and-private-symbols.md)。

### <a name="span-idexiting_dbhspanspan-idexiting_dbhspanexiting-dbh"></a><span id="exiting_dbh"></span><span id="EXITING_DBH"></span>正在退出 THIS->DBH

若要退出 THIS->DBH，请在 THIS->DBH 提示符下使用 **q** 命令。

 

 





