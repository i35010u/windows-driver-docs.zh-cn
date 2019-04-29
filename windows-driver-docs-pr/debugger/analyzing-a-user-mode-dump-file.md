---
title: 分析用户模式转储文件
description: 分析用户模式转储文件
ms.assetid: b7f3dff8-cd2d-41c9-83ff-f0e5fb2312c0
keywords:
- 转储文件，分析用户模式转储文件
ms.date: 08/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: bddd41827cba6ef3e70711b5376c89b14ab17222
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355426"
---
# <a name="analyzing-a-user-mode-dump-file"></a>分析用户模式转储文件

本主题包括以下内容：

- [分析具有 WinDbg 的用户模式转储文件](#windbg)
- [分析具有 CDB 的用户模式转储文件](#cdb)


## <a name="span-idwindbgspanspan-idwindbgspananalyzing-a-user-mode-dump-file-with-windbg"></a><span id="windbg"></span><span id="WINDBG"></span>分析具有 WinDbg 的用户模式转储文件


可以通过 WinDbg 分析用户模式内存转储文件。 处理器或创建转储文件的 Windows 版本不需要在其运行 WinDbg 平台相匹配。

### <a name="span-idinstallingsymbolfilesspanspan-idinstallingsymbolfilesspaninstalling-symbol-files"></a><span id="installing_symbol_files"></span><span id="INSTALLING_SYMBOL_FILES"></span>安装符号文件

分析内存转储文件前, 你需要安装生成转储文件的 Windows 版本的符号文件。 选择要用于分析转储文件调试程序将使用这些文件。 有关符号文件的正确安装的详细信息，请参阅[安装 Windows 符号文件](installing-windows-symbol-files.md)。

此外需要安装的用户模式进程，所有符号文件的应用程序或系统服务，导致系统生成的转储文件。 如果您编写此代码时，符号文件应已生成代码时编译和链接时。 如果这是商业代码，检查产品 CD-ROM 上或与软件制造商联系以这些特定的符号文件。

### <a name="span-idstartingwindbgspanspan-idstartingwindbgspanstarting-windbg"></a><span id="starting_windbg"></span><span id="STARTING_WINDBG"></span>启动 WinDbg

若要分析的转储文件，启动的 WinDbg **z**命令行选项：

**windbg -y** *SymbolPath* **-i** *ImagePath* **-z** *DumpFileName*

**-V**选项 （详细模式） 也是很有用。 有关选项的完整列表，请参阅[ **WinDbg 命令行选项**](windbg-command-line-options.md)。

如果 WinDbg 已在运行和处于休眠模式，则可以通过选择打开故障转储**文件 |打开故障转储**菜单命令或按 CTRL + D 快捷方式键。 当**打开故障转储**出现对话框，请输入完整路径和崩溃转储文件中的名称**文件名**文本框中或使用对话框中选择正确的路径和文件名称。 选择适当的文件后，单击**打开**。

通过使用运行调试器后，还可以打开转储文件[ **.opendump （打开转储文件）** ](-opendump--open-dump-file-.md)命令，然后使用[ **g （转向）** ](g--go-.md).

就可以同时调试多个转储文件。 这可以通过包含多个**z**打开命令行中 （每个后跟一个不同的文件名称），或通过使用[ **.opendump** ](-opendump--open-dump-file-.md)以添加更多的转储文件作为调试器的目标。 有关如何控制多个目标会话的信息，请参阅[调试多个目标](debugging-multiple-targets.md)。

以扩展.dmp 或.mdmp 通常结尾转储文件。 可以使用网络共享或通用命名约定 (UNC) 文件名的内存转储文件。

它也很常见的转储文件，将打包为 CAB 文件。 如果之后指定文件的名称 （包括.cab 扩展名） **z**选项或作为参数[ **.opendump** ](-opendump--open-dump-file-.md)命令，调试器可以读取的转储文件直接从 CAB。 但是，如果有多个转储文件存储在单个 CAB，调试器才能够读取其中之一。 调试器将从 CAB，读取的任何其他文件，即使它们是一样的符号文件或可执行文件与转储文件关联。

### <a name="span-idanalyzingafulluserdumpfilespanspan-idanalyzingafulluserdumpfilespananalyzing-a-full-user-dump-file"></a><span id="analyzing_a_full_user_dump_file"></span><span id="ANALYZING_A_FULL_USER_DUMP_FILE"></span>分析完整的用户转储文件

完整的用户转储文件的分析是类似于一个实时调试会话的分析。 请参阅[调试器命令](debugger-commands.md)引用部分了解详细信息的命令是可用于调试转储文件在用户模式下。

### <a name="span-idanalyzingminidumpfilesspanspan-idanalyzingminidumpfilesspananalyzing-minidump-files"></a><span id="analyzing_minidump_files"></span><span id="ANALYZING_MINIDUMP_FILES"></span>分析信息的小型转储文件

用户模式的小型转储文件的分析是完全用户转储的方式相同。 但是，由于大大降低内存已被预留，您是更受限的可执行的操作。 尝试访问超过小型转储文件中保留的内存的命令将无法正常工作。

### <a name="span-idadditionaltechniquesspanspan-idadditionaltechniquesspanadditional-techniques"></a><span id="additional_techniques"></span><span id="ADDITIONAL_TECHNIQUES"></span>其他技术

有关可用于从转储文件中读取特定类型的信息的方法，请参见[转储文件中提取信息](extracting-information-from-a-dump-file.md)。


## <a name="span-idcdbspanspan-idcdbspananalyzing-a-user-mode-dump-file-with-cdb"></a><span id="cdb"></span><span id="CDB"></span>分析具有 CDB 的用户模式转储文件

可以通过 CDB 分析用户模式内存转储文件。 处理器或创建转储文件的 Windows 版本不需要在其运行 CDB 平台相匹配。

### <a name="span-idinstallingsymbolfilesspanspan-idinstallingsymbolfilesspaninstalling-symbol-files"></a><span id="installing_symbol_files"></span><span id="INSTALLING_SYMBOL_FILES"></span>安装符号文件

分析内存转储文件前, 你需要安装生成转储文件的 Windows 版本的符号文件。 选择要用于分析转储文件调试程序将使用这些文件。 有关符号文件的正确安装的详细信息，请参阅[安装 Windows 符号文件](installing-windows-symbol-files.md)。

此外需要安装的用户模式进程，所有符号文件的应用程序或系统服务，导致系统生成的转储文件。 如果您编写此代码时，符号文件应已生成代码时编译和链接时。 如果这是商业代码，检查产品 CD-ROM 上或与软件制造商联系以这些特定的符号文件。

### <a name="span-idstartingcdbspanspan-idstartingcdbspanstarting-cdb"></a><span id="starting_cdb"></span><span id="STARTING_CDB"></span>起始 CDB

若要分析的转储文件，启动与 CDB **z**命令行选项：

**cdb -y** *SymbolPath* **-i** *ImagePath* **-z** *DumpFileName*

**-V**选项 （详细模式） 也是很有用。 有关选项的完整列表，请参阅[ **CDB 命令行选项**](cdb-command-line-options.md)。

通过使用运行调试器后，还可以打开转储文件[ **.opendump （打开转储文件）** ](-opendump--open-dump-file-.md)命令，然后使用[ **g （转向）** ](g--go-.md). 这样，您可以同时调试多个转储文件。

就可以同时调试多个转储文件。 这可以通过包含多个**z**打开命令行中 （每个后跟一个不同的文件名称），或通过使用[ **.opendump** ](-opendump--open-dump-file-.md)以添加更多的转储文件作为调试器的目标。 有关如何控制多个目标会话的信息，请参阅[调试多个目标](debugging-multiple-targets.md)。

以扩展.dmp 或.mdmp 通常结尾转储文件。 可以使用网络共享或通用命名约定 (UNC) 文件名的内存转储文件。

它也很常见的转储文件，将打包为 CAB 文件。 如果之后指定文件的名称 （包括.cab 扩展名） **z**选项或作为参数[ **.opendump** ](-opendump--open-dump-file-.md)命令，调试器可以读取的转储文件直接从 CAB。 但是，如果有多个转储文件存储在单个 CAB，调试器才能够读取其中之一。 调试器将从 CAB，读取的任何其他文件，即使它们是符号文件或可执行文件与转储文件关联。

### <a name="span-idanalyzingafulluserdumpfilespanspan-idanalyzingafulluserdumpfilespananalyzing-a-full-user-dump-file"></a><span id="analyzing_a_full_user_dump_file"></span><span id="ANALYZING_A_FULL_USER_DUMP_FILE"></span>分析完整的用户转储文件

完整的用户转储文件的分析是类似于一个实时调试会话的分析。 请参阅[调试器命令](debugger-commands.md)引用部分了解详细信息的命令是可用于调试转储文件在用户模式下。

### <a name="span-idanalyzingminidumpfilesspanspan-idanalyzingminidumpfilesspananalyzing-minidump-files"></a><span id="analyzing_minidump_files"></span><span id="ANALYZING_MINIDUMP_FILES"></span>分析信息的小型转储文件

用户模式的小型转储文件的分析是完全用户转储的方式相同。 但是，由于大大降低内存已被预留，您是更受限的可执行的操作。 尝试访问超过小型转储文件中保留的内存的命令将无法正常工作。

### <a name="span-idadditionaltechniquesspanspan-idadditionaltechniquesspanadditional-techniques"></a><span id="additional_techniques"></span><span id="ADDITIONAL_TECHNIQUES"></span>其他技术

有关可用于从转储文件中读取特定类型的信息的方法，请参见[转储文件中提取信息](extracting-information-from-a-dump-file.md)。




 

 





