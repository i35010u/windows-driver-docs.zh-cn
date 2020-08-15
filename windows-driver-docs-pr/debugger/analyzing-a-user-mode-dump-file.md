---
title: 分析用户模式转储文件
description: 分析用户模式转储文件
ms.assetid: b7f3dff8-cd2d-41c9-83ff-f0e5fb2312c0
keywords:
- 转储文件，分析用户模式转储文件
ms.date: 08/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6c458cff99c462023655669ee422e9c5445b7c9d
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88253091"
---
# <a name="analyzing-a-user-mode-dump-file"></a>分析用户模式转储文件

本主题包括以下内容：

- [使用 WinDbg 分析用户模式转储文件](#windbg)
- [使用 CDB 分析用户模式转储文件](#cdb)


## <a name="span-idwindbgspanspan-idwindbgspananalyzing-a-user-mode-dump-file-with-windbg"></a><span id="windbg"></span><span id="WINDBG"></span>使用 WinDbg 分析用户模式转储文件


用户模式内存转储文件可由 WinDbg 进行分析。 创建转储文件的处理器或 Windows 版本不需要与运行 WinDbg 的平台匹配。

### <a name="span-idinstalling_symbol_filesspanspan-idinstalling_symbol_filesspaninstalling-symbol-files"></a><span id="installing_symbol_files"></span><span id="INSTALLING_SYMBOL_FILES"></span>安装符号文件

在分析内存转储文件之前，您将需要安装生成转储文件的 Windows 版本的符号文件。 选择用于分析转储文件的调试器将使用这些文件。 有关正确安装符号文件的详细信息，请参阅 [安装 Windows 符号文件](installing-windows-symbol-files.md)。

还需要安装导致系统生成转储文件的用户模式进程（应用程序或系统服务）的所有符号文件。 如果你编写了此代码，则在编译和链接代码时，应生成符号文件。 如果这是商业代码，请查看产品 cd-rom，或与软件制造商联系以获取这些特定的符号文件。

### <a name="span-idstarting_windbgspanspan-idstarting_windbgspanstarting-windbg"></a><span id="starting_windbg"></span><span id="STARTING_WINDBG"></span>开始 WinDbg

若要分析转储文件，请使用 **-z** 命令行选项启动 WinDbg：

**windbg-y** *SymbolPath* **-i** *ImagePath* **-z** *DumpFileName*

**-V**选项 (详细模式) 也很有用。 有关选项的完整列表，请参阅 [**WinDbg 命令行选项**](windbg-command-line-options.md)。

如果 WinDbg 已经在运行且处于休眠模式，则可以通过选择文件来打开故障转储 **打开故障转储** 菜单命令或按 CTRL + D 快捷键。 出现 " **打开故障转储** " 对话框时，请在 " **文件名** " 文本框中输入故障转储文件的完整路径和名称，或使用对话框选择正确的路径和文件名。 选择了正确的文件后，选择 " **打开**"。

你还可以在运行调试器后使用 [**. opendump (打开转储文件) **](-opendump--open-dump-file-.md) 命令打开转储文件，并在 [**g (中转) **](g--go-.md)。

可以同时调试多个转储文件。 为此，可以在命令行中包含多个 **z** 开关 (每个开关后面跟有不同的文件名) ，或使用 [**opendump**](-opendump--open-dump-file-.md) 将其他转储文件添加为调试器目标。 有关如何控制多目标会话的信息，请参阅 [调试多个目标](debugging-multiple-targets.md)。

转储文件通常以 dmp 或 .mdmp 结尾。 可以为内存转储文件使用网络共享或通用命名约定 (UNC) 文件名。

还经常将转储文件打包到 CAB 文件中。 如果指定文件名 (在 **-z** 选项后包含 .cab 扩展名) ，或指定为 [**opendump**](-opendump--open-dump-file-.md) 命令的参数，则调试器可以直接从 cab 读取转储文件。 但是，如果有多个转储文件存储在一个 CAB 中，则调试器将只能读取其中一个文件。 调试器不会从 CAB 读取任何其他文件，即使它们是与转储文件关联的符号文件或可执行文件。

### <a name="span-idanalyzing_a_full_user_dump_filespanspan-idanalyzing_a_full_user_dump_filespananalyzing-a-full-user-dump-file"></a><span id="analyzing_a_full_user_dump_file"></span><span id="ANALYZING_A_FULL_USER_DUMP_FILE"></span>分析完整用户转储文件

分析完整用户转储文件类似于分析实时调试会话。 有关可用于在用户模式下调试转储文件的命令的详细信息，请参阅 " [调试器命令](debugger-commands.md) 参考" 部分。

### <a name="span-idanalyzing_minidump_filesspanspan-idanalyzing_minidump_filesspananalyzing-minidump-files"></a><span id="analyzing_minidump_files"></span><span id="ANALYZING_MINIDUMP_FILES"></span>分析小型转储文件

用户模式的小型转储文件的分析方式与完全用户转储相同。 不过，由于保留的内存要少得多，因此你可以执行的操作会受到更多的限制。 尝试访问超出小型转储文件中的内存的命令将无法正常运行。

### <a name="span-idadditional_techniquesspanspan-idadditional_techniquesspanadditional-techniques"></a><span id="additional_techniques"></span><span id="ADDITIONAL_TECHNIQUES"></span>其他技术

有关可用于从转储文件中读取特定类型信息的方法，请参阅 [从转储文件提取信息](extracting-information-from-a-dump-file.md)。


## <a name="span-idcdbspanspan-idcdbspananalyzing-a-user-mode-dump-file-with-cdb"></a><span id="cdb"></span><span id="CDB"></span>使用 CDB 分析用户模式转储文件

用户模式内存转储文件可通过 CDB 进行分析。 创建转储文件的处理器或 Windows 版本不需要与运行 CDB 的平台匹配。

### <a name="span-idinstalling_symbol_filesspanspan-idinstalling_symbol_filesspaninstalling-symbol-files"></a><span id="installing_symbol_files"></span><span id="INSTALLING_SYMBOL_FILES"></span>安装符号文件

在分析内存转储文件之前，您将需要安装生成转储文件的 Windows 版本的符号文件。 选择用于分析转储文件的调试器将使用这些文件。 有关正确安装符号文件的详细信息，请参阅 [安装 Windows 符号文件](installing-windows-symbol-files.md)。

还需要安装导致系统生成转储文件的用户模式进程（应用程序或系统服务）的所有符号文件。 如果你编写了此代码，则在编译和链接代码时，应生成符号文件。 如果这是商业代码，请查看产品 cd-rom，或与软件制造商联系以获取这些特定的符号文件。

### <a name="span-idstarting_cdbspanspan-idstarting_cdbspanstarting-cdb"></a><span id="starting_cdb"></span><span id="STARTING_CDB"></span>启动 CDB

若要分析转储文件，请使用 **-z** 命令行选项启动 CDB：

**cdb-y** *SymbolPath* **-i** *ImagePath* **-z** *DumpFileName*

**-V**选项 (详细模式) 也很有用。 有关选项的完整列表，请参阅 [**CDB 命令行选项**](cdb-command-line-options.md)。

你还可以在运行调试器后使用 [**. opendump (打开转储文件) **](-opendump--open-dump-file-.md) 命令打开转储文件，并在 [**g (中转) **](g--go-.md)。 这允许同时调试多个转储文件。

可以同时调试多个转储文件。 为此，可以在命令行中包含多个 **z** 开关 (每个开关后面跟有不同的文件名) ，或使用 [**opendump**](-opendump--open-dump-file-.md) 将其他转储文件添加为调试器目标。 有关如何控制多目标会话的信息，请参阅 [调试多个目标](debugging-multiple-targets.md)。

转储文件通常以 dmp 或 .mdmp 结尾。 可以为内存转储文件使用网络共享或通用命名约定 (UNC) 文件名。

还经常将转储文件打包到 CAB 文件中。 如果指定文件名 (在 **-z** 选项后包含 .cab 扩展名) ，或指定为 [**opendump**](-opendump--open-dump-file-.md) 命令的参数，则调试器可以直接从 cab 读取转储文件。 但是，如果有多个转储文件存储在一个 CAB 中，则调试器将只能读取其中一个文件。 调试器不会从 CAB 读取任何其他文件，即使它们是与转储文件关联的符号文件或可执行文件。

### <a name="span-idanalyzing_a_full_user_dump_filespanspan-idanalyzing_a_full_user_dump_filespananalyzing-a-full-user-dump-file"></a><span id="analyzing_a_full_user_dump_file"></span><span id="ANALYZING_A_FULL_USER_DUMP_FILE"></span>分析完整用户转储文件

分析完整用户转储文件类似于分析实时调试会话。 有关可用于在用户模式下调试转储文件的命令的详细信息，请参阅 " [调试器命令](debugger-commands.md) 参考" 部分。

### <a name="span-idanalyzing_minidump_filesspanspan-idanalyzing_minidump_filesspananalyzing-minidump-files"></a><span id="analyzing_minidump_files"></span><span id="ANALYZING_MINIDUMP_FILES"></span>分析小型转储文件

用户模式的小型转储文件的分析方式与完全用户转储相同。 不过，由于保留的内存要少得多，因此你可以执行的操作会受到更多的限制。 尝试访问超出小型转储文件中的内存的命令将无法正常运行。

### <a name="span-idadditional_techniquesspanspan-idadditional_techniquesspanadditional-techniques"></a><span id="additional_techniques"></span><span id="ADDITIONAL_TECHNIQUES"></span>其他技术

有关可用于从转储文件中读取特定类型信息的方法，请参阅 [从转储文件提取信息](extracting-information-from-a-dump-file.md)。




 

 





