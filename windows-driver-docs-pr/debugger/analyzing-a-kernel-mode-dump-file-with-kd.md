---
title: 使用 KD 分析内核模式转储文件
description: 使用 KD 分析内核模式转储文件
ms.assetid: 7e8fbf6e-0adc-434c-ba93-f83f49a4af92
keywords:
- KD，分析转储文件
- 包含转储文件，分析与 KD 内核模式转储文件的 CAB 文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dda7b0529f1523625ad6cb0563bde2e45ac5a7f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562713"
---
# <a name="analyzing-a-kernel-mode-dump-file-with-kd"></a>使用 KD 分析内核模式转储文件


## <span id="ddk_analyzing_a_kernel_mode_dump_file_with_kd_dbg"></span><span id="DDK_ANALYZING_A_KERNEL_MODE_DUMP_FILE_WITH_KD_DBG"></span>


可以通过 KD 分析内核模式内存转储文件。 处理器或创建转储文件的 Windows 版本不需要在其运行 KD 平台相匹配。

### <a name="span-idstartingkdspanspan-idstartingkdspanstarting-kd"></a><span id="starting_kd"></span><span id="STARTING_KD"></span>起始 KD

若要分析的转储文件，启动与 KD **z**命令行选项：

**kd -y** *SymbolPath* **-i** *ImagePath* **-z** *DumpFileName*

**-V**选项 （详细模式） 也是很有用。 有关选项的完整列表，请参阅[ **KD 命令行选项**](kd-command-line-options.md)。

通过使用运行调试器后，还可以打开转储文件[ **.opendump （打开转储文件）** ](-opendump--open-dump-file-.md)命令，然后使用[ **g （转向）** ](g--go-.md).

就可以同时调试多个转储文件。 这可以通过包含多个**z**打开命令行中 （每个后跟一个不同的文件名称），或通过使用[ **.opendump** ](-opendump--open-dump-file-.md)以添加更多的转储文件作为调试器的目标。 有关如何控制多个目标会话的信息，请参阅[调试多个目标](debugging-multiple-targets.md)。

以扩展.dmp 或.mdmp 通常结尾转储文件。 可以使用网络共享或通用命名约定 (UNC) 文件名的内存转储文件。

它也很常见的转储文件，将打包为 CAB 文件。 如果之后指定文件的名称 （包括.cab 扩展名） **z**选项或作为参数[ **.opendump** ](-opendump--open-dump-file-.md)命令，调试器可以读取的转储文件直接从 CAB。 但是，如果有多个转储文件存储在单个 CAB，调试器才能够读取其中之一。 调试器将从 CAB，读取的任何其他文件，即使它们是一样的符号文件或使用转储文件关联的其他文件。

### <a name="span-idanalyzingthedumpfilespanspan-idanalyzingthedumpfilespananalyzing-the-dump-file"></a><span id="analyzing_the_dump_file"></span><span id="ANALYZING_THE_DUMP_FILE"></span>分析转储文件

如果您正在分析内核内存转储或小的内存转储，你可能需要设置以指向可能加载在内存中的故障时的任何可执行文件的可执行映像路径。

类似于一个实时调试会话的分析转储文件的分析。 请参阅[调试器命令](debugger-commands.md)引用部分了解详细信息的命令是可用于调试在内核模式转储文件。

在大多数情况下，你应该开始使用[ **！ 分析**](-analyze.md)。 此扩展命令执行的转储文件的自动分析，并通常可能会导致很多有用信息。

[ **.Bugcheck （显示 Bug 检查数据）** ](-bugcheck--display-bug-check-data-.md)显示 bug 检查代码和其参数。 查找在此 bug 检查[Bug 检查代码参考](bug-check-code-reference2.md)特定错误有关的信息。

下面的调试器扩展是用于分析的内核模式崩溃转储特别有用：

[**!drivers**](-drivers.md)

[**!kdext\*.locks**](-locks---kdext--locks-.md)

[**!memusage**](-memusage.md)

[**!vm**](-vm.md)

[**!errlog**](-errlog.md)

[**!process 0 0**](-process.md)

[**!process 0 7**](-process.md)

有关可用于从转储文件中读取特定类型的信息的方法，请参见[转储文件中提取信息](extracting-information-from-a-dump-file.md)。

 

 





