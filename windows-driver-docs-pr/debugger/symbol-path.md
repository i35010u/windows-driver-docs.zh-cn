---
title: Windows 调试器的符号路径
description: 符号路径指定 Windows 调试器（WinDbg，KD，CDB，NTST）查找符号文件的位置。
ms.assetid: 705df98f-717f-40ad-a424-101826970691
keywords: 符号文件和路径，符号，延迟符号加载，延迟符号加载，符号路径
ms.date: 10/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 433f34062c372b6226bf833baddd95255c3cdfbc
ms.sourcegitcommit: d2dab8b8bf335835d0341ca3f0a36eab0ec028f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72892679"
---
# <a name="symbol-path-for-windows-debuggers"></a>Windows 调试器的符号路径

符号路径指定 Windows 调试器（WinDbg，KD，CDB，NTST）查找符号文件的位置。 有关符号和符号文件的详细信息，请参阅[符号](symbols.md)。

一些编译器（如 Microsoft Visual Studio）将符号文件放在二进制文件所在的同一目录中。 符号文件和检查后的二进制文件包含路径和文件名信息。 此信息通常使调试器能够自动找到符号文件。 如果要在生成可执行文件的计算机上调试用户模式进程，并且符号文件仍在其原始位置，则调试器可以在不设置符号路径的情况下找到符号文件。

在大多数其他情况下，必须将符号路径设置为指向符号文件位置。

## <a name="span-idsymbol_path_syntaxspanspan-idsymbol_path_syntaxspanspan-idsymbol_path_syntaxspansymbol-path-syntax"></a><span id="Symbol_Path_Syntax"></span><span id="symbol_path_syntax"></span><span id="SYMBOL_PATH_SYNTAX"></span>符号路径语法

调试器的符号路径是由多个目录路径组成的字符串，由分号分隔。

支持相对路径。 但是，除非始终从同一目录启动调试器，否则应在每个路径之前添加驱动器号或网络共享。 还支持网络共享。

对于符号路径中的每个目录，调试器都将查找三个目录。 例如，如果符号路径包含 `c:\MyDir` 目录，并且调试器正在查找 DLL 的符号信息，则调试器首先查找 `c:\MyDir\symbols\dll`，然后在 `c:\MyDir\dll`，最后在 `c:\MyDir` 中查找。 然后，调试器为符号路径中的每个目录重复此进程。 最后，调试程序将在当前目录中查找，然后在当前目录中的后面追加 `..\dll`。 （调试器将追加 `..\dll`、`..\exe` 或 `..\sys`，具体取决于正在调试的二进制文件。）

符号文件具有日期和时间戳。 您不必担心调试器将使用在此序列中首先可能会找到的错误符号。 它始终查找与正在调试的二进制文件上的时间戳匹配的符号。 有关符号文件不可用时的响应的详细信息，请参阅[补偿符号匹配问题](matching-symbol-names.md)。

设置符号路径的一种方法是输入[**sympath**](-sympath--set-symbol-path-.md)命令。 有关设置符号路径的其他方式，请参阅本主题后面的[控制符号路径](#controlling-the-symbol-path)。

## <a name="span-idcaching_symbols_locallyspanspan-idcaching_symbols_locallyspanspan-idcaching_symbols_locallyspancaching-symbols-locally"></a><span id="Caching_Symbols_Locally"></span><span id="caching_symbols_locally"></span><span id="CACHING_SYMBOLS_LOCALLY"></span>在本地缓存符号

强烈建议您始终在本地缓存符号。 在本地缓存符号的一种方法是在符号路径中包含 `cache*;` 或 `cache*localsymbolcache;*`。

如果在符号路径中包含字符串 `cache*;`，则从出现在此字符串右侧的任何元素加载的符号将存储在本地计算机上的默认符号缓存目录中。 例如，以下命令通知调试器从网络共享获取符号 `\\someshare` 并缓存本地计算机上默认位置中的符号。

```dbgcmd
.sympath cache*;\\someshare
```

如果在符号路径中包含字符串 `cache*localsymbolcache;`，则从出现在此字符串右侧的任何元素加载的符号将存储在*localsymbolcache*目录中。

例如，以下命令通知调试器从网络共享获取符号 `\\someshare` 并缓存 `c:\MySymbols` 目录中的符号。

```dbgcmd
.sympath cache*c:\MySymbols;\\someshare
```

## <a name="span-idusing_a_symbol_serverspanspan-idusing_a_symbol_serverspanspan-idusing_a_symbol_serverspanusing-a-symbol-server"></a><span id="Using_a_Symbol_Server"></span><span id="using_a_symbol_server"></span><span id="USING_A_SYMBOL_SERVER"></span>使用符号服务器

如果已连接到 Internet 或企业网络，则访问符号的最有效方法是使用符号服务器。 您可以通过使用符号路径中的 `srv*`、`srv*symbolstore` 或 `srv*localsymbolcache*symbolstore` 字符串来使用符号服务器。

如果在符号路径中包含字符串 `srv*`，则调试器将使用符号服务器从默认符号存储区中获取符号。 例如，以下命令通知调试器使用符号服务器从默认符号存储区中获取符号。 这些符号不会缓存在本地计算机上。

```dbgcmd
.sympath srv*
```

如果在符号路径中包含字符串 `srv*symbolstore`，则调试器将使用符号服务器从*symbolstore*存储区中获取符号。 例如，以下命令通知调试器使用符号服务器从符号存储区中的 https://msdl.microsoft.com/download/symbols 获取符号。 这些符号不会缓存在本地计算机上。

```dbgcmd
.sympath srv*https://msdl.microsoft.com/download/symbols
```

如果在符号路径中包含字符串 `srv*localcache*symbolstore`，则调试器使用符号服务器从*symbolstore*存储区中获取符号，并将它们缓存在*localcache*目录中。 例如，下面的命令通知调试器使用符号服务器从符号存储区中获取符号，并在 `c:\MyServerSymbols` 中缓存符号 https://msdl.microsoft.com/download/symbols 。

```dbgcmd
.sympath srv*c:\MyServerSymbols*https://msdl.microsoft.com/download/symbols
```

如果计算机上的某个目录手动放置符号，则不要将该目录用作从符号服务器获取的符号的缓存。 相反，请使用两个不同的目录。 例如，你可以将符号手动置于 `c:\MyRegularSymbols` 中，然后将 `c:\MyServerSymbols` 指定为从服务器获取的符号的缓存。 下面的示例演示如何在符号路径中指定两个目录。

```dbgcmd
.sympath c:\MyRegularSymbols;srv*c:\MyServerSymbols*https://msdl.microsoft.com/download/symbols
```

有关符号服务器的详细信息，请参阅[符号存储和符号服务器](symbol-stores-and-symbol-servers.md)。

## <a name="span-idcombining_cache__and_srv_spanspan-idcombining_cache__and_srv_spanspan-idcombining_cache__and_srv_spancombining-cache-and-srv"></a><span id="Combining_cache__and_srv_"></span><span id="combining_cache__and_srv_"></span><span id="COMBINING_CACHE__AND_SRV_"></span>合并缓存 \* 和 srv \*


如果在符号路径中包含字符串 `cache*;`，则从出现在此字符串右侧的任何元素加载的符号将存储在本地计算机上的默认符号缓存目录中。 例如，下面的命令通知调试器使用符号服务器从存储 https://msdl.microsoft.com/download/symbols 区获取符号，并将它们缓存在默认的符号缓存目录中。

```dbgcmd
.sympath cache*;srv*https://msdl.microsoft.com/download/symbols
```

如果在符号路径中包含字符串 `cache*localsymbolcache;`，则从出现在此字符串右侧的任何元素加载的符号将存储在*localsymbolcache*目录中。

例如，下面的命令通知调试器使用符号服务器从存储区获取符号 https://msdl.microsoft.com/download/symbols 并缓存 `c:\MySymbols` 目录中的符号。

```dbgcmd
.sympath cache*c:\MySymbols;srv*https://msdl.microsoft.com/download/symbols
```

## <a name="span-idusing_agestore_to_reduce_the_cache_sizespanspan-idusing_agestore_to_reduce_the_cache_sizespanusing-agestore-to-reduce-the-cache-size"></a><span id="using_agestore_to_reduce_the_cache_size"></span><span id="USING_AGESTORE_TO_REDUCE_THE_CACHE_SIZE"></span>使用 AgeStore 减少缓存大小

你可以使用 AgeStore 工具删除早于指定日期的缓存文件，或删除足够的旧文件，使缓存的大小小于指定的数量。 如果下游存储太大，这可能很有用。 有关详细信息，请参阅[AgeStore](agestore.md)。

有关符号服务器和符号存储的详细信息，请参阅[符号存储和符号服务器](symbol-stores-and-symbol-servers.md)。

## <a name="span-idlazy_symbol_loadingspanspan-idlazy_symbol_loadingspanlazy-symbol-loading"></a><span id="lazy_symbol_loading"></span><span id="LAZY_SYMBOL_LOADING"></span>延迟符号加载

调试器的默认行为是使用*延迟符号加载*（也称为*延迟符号加载*）。 这种类型的加载意味着符号只有在需要时才会加载。

当符号路径发生更改时（例如，通过使用[`.sympath`](-sympath--set-symbol-path-.md)命令），将会惰式重载包含导出符号的所有加载的模块。

如果新路径不再包含用于加载 PDB 符号的原始路径，则将会惰式重载包含完整 PDB 符号的模块的符号。 如果新路径仍包含 PDB 符号文件的原始路径，则不会惰式重载这些符号。

有关延迟符号加载的详细信息，请参阅[延迟符号加载](deferred-symbol-loading.md)。

可以通过使用 `-s`[命令行选项](command-line-options.md)来关闭 CDB 和 KD 中的延迟符号加载。 还可以通过使用 `ld` [ **（加载符号）** ](ld--load-symbols-.md)命令或使用 `.reload` [ **（重新加载模块）** ](-reload--reload-module-.md)命令以及 `/f` 选项来强制执行符号加载。

## <a name="span-idazurespanspan-idazurespanazure-devops-services-artifacts"></a><span id="azure"></span><span id="AZURE"></span>Azure DevOps Services 项目

符号服务器可用于 Azure DevOps Services 中的 Azure Artifacts。 有关在 WinDbg 中使用 Azure Artifacts 的信息，请参阅[在 windbg 中使用符号进行调试](https://docs.microsoft.com/azure/devops/artifacts/symbols/debug-with-symbols-visual-studio)。 有关 Azure 生成的符号的一般信息，请参阅[符号文件（pdb）](https://docs.microsoft.com/azure/devops/artifacts/concepts/symbols)。

### <a name="span-idcontrolling-the-symbol-pathspanspan-idcontrolling-the-symbol-pathspancontrolling-the-symbol-path"></a><span id="controlling-the-symbol-path"></span><span id="CONTROLLING-THE-SYMBOL-PATH"></span>控制符号路径

若要控制符号路径，可以执行以下操作之一：

- 使用[`.sympath`](-sympath--set-symbol-path-.md)命令来显示、设置、更改或附加到路径。 `.symfix` [ **（设置符号存储路径）** ](-symfix--set-symbol-store-path-.md)命令类似于 `.sympath` 但会保存某些键入内容。

- 在启动调试器之前，请使用 `_NT_SYMBOL_PATH` 和 `_NT_ALT_SYMBOL_PATH`[环境变量](environment-variables.md)来设置路径。 符号路径是通过在 `_NT_ALT_SYMBOL_PATH`后面追加 `_NT_SYMBOL_PATH` 来创建的。 （通常，路径通过 `_NT_SYMBOL_PATH`设置。 但是，在特殊情况下，你可能想要使用 `_NT_ALT_SYMBOL_PATH` 重写这些设置，如共享符号文件的私有版本。）如果尝试通过这些环境变量添加无效目录，调试器将忽略此目录。

- 启动调试器时，使用 `-y`[命令行选项](command-line-options.md)来设置路径。

- （仅限 WinDbg）使用[文件 |符号文件路径](file---symbol-file-path.md)命令或按 `CTRL+S` 显示、设置、更改或附加到路径。

如果使用 `-sins`[命令行选项](command-line-options.md)，调试器将忽略符号路径环境变量。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[高级 SymSrv 使用](advanced-symsrv-use.md)
