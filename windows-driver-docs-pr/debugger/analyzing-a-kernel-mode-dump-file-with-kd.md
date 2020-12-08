---
title: 使用 KD 分析内核模式转储文件
description: 使用 KD 分析内核模式转储文件
keywords:
- KD，分析转储文件
- 包含转储文件的 CAB 文件，使用 KD 分析内核模式转储文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81dd23a0d30dc9c9be0dfbc958d1e188c399c797
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813325"
---
# <a name="analyzing-a-kernel-mode-dump-file-with-kd"></a>使用 KD 分析内核模式转储文件


## <span id="ddk_analyzing_a_kernel_mode_dump_file_with_kd_dbg"></span><span id="DDK_ANALYZING_A_KERNEL_MODE_DUMP_FILE_WITH_KD_DBG"></span>


可以通过 KD 分析内核模式内存转储文件。 创建转储文件的处理器或 Windows 版本不需要与运行 KD 的平台匹配。

### <a name="span-idstarting_kdspanspan-idstarting_kdspanstarting-kd"></a><span id="starting_kd"></span><span id="STARTING_KD"></span>启动 KD

若要分析转储文件，请使用 **-z** 命令行选项启动 KD：

**kd-y** *SymbolPath* **-i** *ImagePath* **-z** *DumpFileName*

**-V** 选项 (详细模式) 也很有用。 有关选项的完整列表，请参阅 [**KD Command-Line 选项**](kd-command-line-options.md)。

你还可以在运行调试器后使用 [**. opendump (打开转储文件)**](-opendump--open-dump-file-.md) 命令打开转储文件，并在 [**g (中转)**](g--go-.md)。

可以同时调试多个转储文件。 为此，可以在命令行中包含多个 **z** 开关 (每个开关后面跟有不同的文件名) ，或使用 [**opendump**](-opendump--open-dump-file-.md) 将其他转储文件添加为调试器目标。 有关如何控制多目标会话的信息，请参阅 [调试多个目标](debugging-multiple-targets.md)。

转储文件通常以 dmp 或 .mdmp 结尾。 可以为内存转储文件使用网络共享或通用命名约定 (UNC) 文件名。

还经常将转储文件打包到 CAB 文件中。 如果指定文件名 (在 **-z** 选项后包含 .cab 扩展名) ，或指定为 [**opendump**](-opendump--open-dump-file-.md) 命令的参数，则调试器可以直接从 cab 读取转储文件。 但是，如果有多个转储文件存储在一个 CAB 中，则调试器将只能读取其中一个文件。 调试器不会从 CAB 读取任何其他文件，即使它们是符号文件或与转储文件关联的其他文件。

### <a name="span-idanalyzing_the_dump_filespanspan-idanalyzing_the_dump_filespananalyzing-the-dump-file"></a><span id="analyzing_the_dump_file"></span><span id="ANALYZING_THE_DUMP_FILE"></span>分析转储文件

如果要分析内核内存转储或小内存转储，可能需要将可执行文件映像路径设置为指向在崩溃时可能已加载到内存中的任何可执行文件。

转储文件的分析类似于分析实时调试会话。 有关可用于在内核模式下调试转储文件的命令的详细信息，请参阅 " [调试器命令](debugger-commands.md) 参考" 部分。

在大多数情况下，应该首先使用 [**！分析**](-analyze.md)。 此扩展命令执行转储文件的自动分析，并可能会导致许多有用的信息。

[**错误检查 (显示 Bug 检查数据)**](-bugcheck--display-bug-check-data-.md)显示 bug 检查代码及其参数。 有关特定错误的信息，请查看 [Bug 检查代码参考](bug-check-code-reference2.md) 中的此 bug 检查。

以下调试器扩展对于分析内核模式故障转储特别有用：

[**lm**](lm--list-loaded-modules-.md)

[**！ kdext \***](-locks---kdext--locks-.md)

[**!memusage**](-memusage.md)

[**！ vm**](-vm.md)

[**!errlog**](-errlog.md)

[**！进程 0 0**](-process.md)

[**！进程 0 7**](-process.md)

有关可用于从转储文件中读取特定类型信息的方法，请参阅 [从转储文件提取信息](extracting-information-from-a-dump-file.md)。

 

 





