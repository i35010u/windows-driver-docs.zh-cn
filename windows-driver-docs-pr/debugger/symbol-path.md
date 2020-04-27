---
title: Windows 调试器的符号路径
description: 符号路径指定 Windows 调试器（WinDbg、KD、CDB、NTST）查找符号文件的位置。
ms.assetid: 705df98f-717f-40ad-a424-101826970691
keywords: 符号文件和路径、符号、延迟符号加载、延迟符号加载、符号路径
ms.date: 10/23/2019
ms.localizationpriority: high
ms.openlocfilehash: 71cf811cffadf33a34c207e5455ff2a0e3d322f6
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "78335964"
---
# <a name="symbol-path-for-windows-debuggers"></a>Windows 调试器的符号路径

符号路径指定 Windows 调试器（WinDbg、KD、CDB、NTST）查找符号文件的位置。 有关符号和符号文件的详细信息，请参阅[符号](symbols.md)。

一些编译器（如 Microsoft Visual Studio）将符号文件与二进制文件放在同一目录中。 符号文件和选中的二进制文件包含路径和文件名信息。 此信息通常使调试器能够自动查找符号文件。 如果要在生成可执行文件的计算机上调试用户模式进程，并且符号文件仍在其原始位置，则调试器可以在不设置符号路径的情况下定位符号文件。

在大多数其他情况下，必须将符号路径设置为指向符号文件位置。

## <a name="span-idsymbol_path_syntaxspanspan-idsymbol_path_syntaxspanspan-idsymbol_path_syntaxspansymbol-path-syntax"></a><span id="Symbol_Path_Syntax"></span><span id="symbol_path_syntax"></span><span id="SYMBOL_PATH_SYNTAX"></span>符号路径语法

调试器的符号路径是由多个目录路径组成的字符串，用分号分隔。

支持相对路径。 但是，除非始终从同一目录启动调试器，否则应在每个路径之前添加驱动程序号或网络共享。 还支持网络共享。

对于符号路径中的每个目录，调试器将在三个目录中查找。 例如，如果符号路径包含 `c:\MyDir` 目录，并且调试器正在查找 DLL 的符号信息，则调试器依次查找 `c:\MyDir\symbols\dll``c:\MyDir\dll``c:\MyDir`。 然后，调试器对符号路径中的每个目录重复此过程。 最后，调试器在当前目录中查找，然后在当前目录中附加 `..\dll`。 （调试器将附加 `..\dll`、`..\exe` 或 `..\sys`，具体取决于正在调试的二进制文件。）

符号文件具有日期和时间戳。 不必担心调试器会使用首先在此序列中找到的错误符号。 它始终查找与正在调试的二进制文件上的时间戳匹配的符号。 有关符号文件不可用时的响应的详细信息，请参阅[补偿符号匹配问题](matching-symbol-names.md)。

设置符号路径的一种方法是输入 [.sympath](-sympath--set-symbol-path-.md) 命令  。 有关设置符号路径的其他方法，请参阅本主题后面的[控制符号路径](#controlling-the-symbol-path)。

## <a name="span-idcaching_symbols_locallyspanspan-idcaching_symbols_locallyspanspan-idcaching_symbols_locallyspancaching-symbols-locally"></a><span id="Caching_Symbols_Locally"></span><span id="caching_symbols_locally"></span><span id="CACHING_SYMBOLS_LOCALLY"></span>在本地缓存符号

强烈建议始终在本地缓存符号。 在本地缓存符号的一种方法是在符号路径中包含 `cache*;` 或 `cache*localsymbolcache;*`。

如果在符号路径中包含字符串 `cache*;`，则从该字符串右侧的任何元素加载的符号都存储在本地计算机的默认符号缓存目录中。 例如，以下命令通知调试器从网络共享 `\\someshare` 中获取符号，并将这些符号缓存在本地计算机上的默认位置。

```dbgcmd
.sympath cache*;\\someshare
```

如果在符号路径中包含字符串 `cache*localsymbolcache;`，则从该字符串右侧出现的任何元素加载的符号都存储在 localsymbolcache 目录中  。

例如，以下命令通知调试器从网络共享 `\\someshare` 中获取符号，并将这些符号缓存在 `c:\MySymbols` 目录中。

```dbgcmd
.sympath cache*c:\MySymbols;\\someshare
```

## <a name="span-idusing_a_symbol_serverspanspan-idusing_a_symbol_serverspanspan-idusing_a_symbol_serverspanusing-a-symbol-server"></a><span id="Using_a_Symbol_Server"></span><span id="using_a_symbol_server"></span><span id="USING_A_SYMBOL_SERVER"></span> 使用符号服务器

如果已连接到 Internet 或公司网络，则访问符号的最有效方法是使用符号服务器。 通过在符号路径中使用 `srv*`、`srv*symbolstore` 或 `srv*localsymbolcache*symbolstore` 字符串，可以使用符号服务器。

如果在符号路径中包含字符串 `srv*`，调试器将使用符号服务器从默认符号存储中获取符号。 例如，以下命令通知调试器使用符号服务器从默认符号存储中获取符号。 这些符号不会缓存在本地计算机上。

```dbgcmd
.sympath srv*
```

如果在符号路径中包含字符串 `srv*symbolstore`，调试器将使用符号服务器从“符号存储”中获取符号  。 例如，以下命令通知调试器使用符号服务器从位于 https://msdl.microsoft.com/download/symbols 的符号存储中获取符号。 这些符号不会缓存在本地计算机上。

```dbgcmd
.sympath srv*https://msdl.microsoft.com/download/symbols
```

如果在符号路径中包含字符串 `srv*localcache*symbolstore`，调试器将使用符号服务器从“符号存储”中获取符号，并将其缓存在“本地缓存”目录中   。 例如，以下命令通知调试器使用符号服务器从位于 https://msdl.microsoft.com/download/symbols 的符号存储中获取符号，并将这些符号缓存在 `c:\MyServerSymbols` 中。

```dbgcmd
.sympath srv*c:\MyServerSymbols*https://msdl.microsoft.com/download/symbols
```

如果计算机上有手动放置符号的目录，请不要将该目录用于缓存从符号服务器获取的符号。 相反，请使用两个不同的目录。 例如，可以手动将符号放在 `c:\MyRegularSymbols` 中，然后指定用 `c:\MyServerSymbols` 缓存从服务器获取的符号。 下面的示例演示如何在符号路径中指定这两个目录。

```dbgcmd
.sympath c:\MyRegularSymbols;srv*c:\MyServerSymbols*https://msdl.microsoft.com/download/symbols
```

有关符号服务器的详细信息，请参阅[符号存储和符号服务器](symbol-stores-and-symbol-servers.md)。

## <a name="span-idcombining_cache__and_srv_spanspan-idcombining_cache__and_srv_spanspan-idcombining_cache__and_srv_spancombining-cache-and-srv"></a><span id="Combining_cache__and_srv_"></span><span id="combining_cache__and_srv_"></span><span id="COMBINING_CACHE__AND_SRV_"></span>合并缓存 和 srv\*\*


如果在符号路径中包含字符串 `cache*;`，则从该字符串右侧的任何元素加载的符号都存储在本地计算机的默认符号缓存目录中。 例如，以下命令通知调试器使用符号服务器从位于 https://msdl.microsoft.com/download/symbols 的存储中获取符号，并将其缓存在默认的符号缓存目录中。

```dbgcmd
.sympath cache*;srv*https://msdl.microsoft.com/download/symbols
```

如果在符号路径中包含字符串 `cache*localsymbolcache;`，则从该字符串右侧出现的任何元素加载的符号都存储在 localsymbolcache 目录中  。

例如，以下命令通知调试器使用符号服务器从位于 https://msdl.microsoft.com/download/symbols 的存储中获取符号，并将这些符号缓存在 `c:\MySymbols` 目录中。

```dbgcmd
.sympath cache*c:\MySymbols;srv*https://msdl.microsoft.com/download/symbols
```

## <a name="span-idusing_agestore_to_reduce_the_cache_sizespanspan-idusing_agestore_to_reduce_the_cache_sizespanusing-agestore-to-reduce-the-cache-size"></a><span id="using_agestore_to_reduce_the_cache_size"></span><span id="USING_AGESTORE_TO_REDUCE_THE_CACHE_SIZE"></span> 使用 AgeStore 减少缓存大小

可以使用 AgeStore 工具删除早于指定日期的缓存文件，或删除足够的旧文件，使缓存的结果大小小于指定的数量。 如果下游存储太大，这可能很有用。 有关详细信息，请参阅 [AgeStore](agestore.md)。

有关符号服务器和符号存储的详细信息，请参阅[符号存储和符号服务器](symbol-stores-and-symbol-servers.md)。

## <a name="span-idlazy_symbol_loadingspanspan-idlazy_symbol_loadingspanlazy-symbol-loading"></a><span id="lazy_symbol_loading"></span><span id="LAZY_SYMBOL_LOADING"></span>延迟符号加载

调试器的默认行为是使用“延迟符号加载”（也称为“延期符号加载”）   。 这种加载意味着在需要时才加载符号。

当符号路径发生更改时（例如使用 [`.sympath`](-sympath--set-symbol-path-.md) 命令更改），包含导出符号的所有已加载模块都将延迟重新加载。

如果新路径不再包含用于加载 PDB 符号的原始路径，则具有完整 PDB 符号的模块符号将延迟重新加载。 如果新路径仍然包含 PDB 符号文件的原始路径，则不会延迟重新加载这些符号。

有关延迟符号加载的详细信息，请参阅[延迟符号加载](deferred-symbol-loading.md)。

通过使用 `-s` [命令行选项](command-line-options.md)，可以关闭 CDB 和 KD 中的延迟符号加载。 还可以通过使用 `ld` [（加载符号）](ld--load-symbols-.md)命令或使用`.reload`[（重新加载模块）](-reload--reload-module-.md)命令和 `/f` 选项来强制加载符号   。

## <a name="span-idazurespanspan-idazurespanazure-devops-services-artifacts"></a><span id="azure"></span><span id="AZURE"></span>Azure DevOps Services Artifacts

符号服务器可用于 Azure DevOps 服务中的 Azure Artifacts。 有关在 WinDbg 中使用 Azure Artifacts 的信息，请参阅[在 WinDbg 中使用符号进行调试](https://docs.microsoft.com/azure/devops/artifacts/symbols/debug-with-symbols-visual-studio)。 有关 Azure 生成的符号的常规信息，请参阅[符号文件 (PDB)](https://docs.microsoft.com/azure/devops/artifacts/concepts/symbols)。

### <a name="span-idcontrolling-the-symbol-pathspanspan-idcontrolling-the-symbol-pathspancontrolling-the-symbol-path"></a><span id="controlling-the-symbol-path"></span><span id="CONTROLLING-THE-SYMBOL-PATH"></span>控制符号路径

若要控制符号路径，可以执行以下操作之一：

- 使用 [`.sympath`](-sympath--set-symbol-path-.md) 命令显示、设置、更改或附加到路径。 `.symfix`[（设置符号存储路径）](-symfix--set-symbol-store-path-.md)命令与 `.sympath` 类似，但会保存某些键入内容  。

- 在启动调试器之前，请使用 `_NT_SYMBOL_PATH` 和 `_NT_ALT_SYMBOL_PATH` [环境变量](environment-variables.md)设置路径。 符号路径是通过在 `_NT_ALT_SYMBOL_PATH` 后附加 `_NT_SYMBOL_PATH` 创建的。 （通常，路径通过 `_NT_SYMBOL_PATH` 设置。 但是，在特殊情况下，例如拥有共享符号文件的专用版本时，可以使用 `_NT_ALT_SYMBOL_PATH` 重写这些设置。）如果尝试通过这些环境变量添加无效目录，调试器将忽略此目录。

- 启动调试器时，使用 `-y` [命令行选项](command-line-options.md)设置路径。

- （仅限 WinDbg）使用 [File | Symbol File Path](file---symbol-file-path.md) 命令或按 `CTRL+S` 显示、设置、更改或附加到路径。

如果使用 `-sins` [命令行选项](command-line-options.md)，调试器将忽略符号路径环境变量。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[SymSrv 的高级用法](advanced-symsrv-use.md)
